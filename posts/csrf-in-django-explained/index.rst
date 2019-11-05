.. title: CSRF in Django Explained
.. slug: csrf-in-django-explained
.. date: 2019-11-05 18:31:37 UTC+05:30
.. tags: 
.. category: 
.. link: 
.. description: 
.. type: text

Going back to the time when I was new to technology, learning to code and had decided to learn Django.

Django is a web framework written in Python and is used for developing web services. There are some well written modules of Django that make it suitable for faster development with better efficiency.
The mistake I was doing is to learn from multiple resources at the same time. It consisted of Youtube tutorials, official documentation, Django-Girls website, Udemy, etc. I was messed up with the settings, project and app configurations, and many of the times are with Django forms. The errors that I find silly now, were really frustrating and used to be not less than a nightmare for me.

What is CSRF?
CSRF stands for Cross-Site Request Forgery. It is an attack that forces an end user to execute unwanted actions on a web application in which they’re currently authenticated.

For example, lets up say this is an URL that is generated when one is trying to complete the payment/transfer process.

    http://www.bank.com/transfer.php?&money=500&transferto=someaccount

the payment or transfer only happens only when the session is already running over the browser. So let’s suppose that you have once logged in to a bank website before. Now cookies and stuff are already stored in your browser then the person can be exploited by sending the transfer URL in a hidden form to the victim, for example, the link is :

    <img src =”http://www.bank.com/transfer.php?&money=500&transferto=attackeraccount” >

The above link is a broken image link, but the moment victim’s browser will try to render the image it will make a request to the image URL, since we have given the malicious link the request will be made and since you are already logged in to bank, the browser’s session and cookie will help it to execute the process and the money might be transferred to the attacker account without getting notified to the victim.

Hence, in order to prevent it, modern web services use a same-origin policy. Django has this built-in feature of providing a token (called as CSRF token) every time a form is submitted that checks if the request is procedure from the same origin.
To make a form submission in Django:-

    <form method =”POST” >

        {% csrf_token %}

        …form body….

    </form>

If you do not add {% csrf_token %} you will get Error 403.
CSRF attack is so *dangerous* that it is listed under the OWASP Top 10 vulnerabilities. It is the kind of vulnerability in which victim’s own browser support in getting exploited. So from a developer perspective, one should never ignore these kinds of vulnerabilities during developing.

References:

    - http://resources.infosecinstitute.com/owasp-csrf/
    - https://www.owasp.org/index.php/Cross-Site_Request_Forgery_(CSRF)

 
    *Please comment for any kind of confusion/suggestions etc. Also Follow me as I write mostly about Python, Blockchain and Web development using Django.*
