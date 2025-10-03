# Oracle Cloud Infrastructure Architect Associate
## Identity Domains
A self-contained IAM service. Act as a container to manage user, roles, federation, SSO, MFA e.t.c.

![](img/ad67.png)

Why do we need multiple ID domains?
Isolation of administrative control, security & compliance and simplified management.
Another advantage of creating another ID domain is that a default user is created to manage that domain. Note that when you create an ID check the default region. Additional domain are not by default replicated to other regions by default, so make sure that you do the replication.


![](img/ad68.png)

some of the default groups are shown in the figure below:

![](img/ad68.png)
