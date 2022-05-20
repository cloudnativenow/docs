### Fork Boutique GitHub Repository

A fork is a copy of a repository so you can leverage someone else's project as a starting point for your own ideas. Forking a repository allows you to freely experiment with changes without affecting the original upstream repository. We are leveraging [Google's Boutique application](https://github.com/GoogleCloudPlatform/microservices-demo) which we forked ourselves earlier under a new repository called `cassandra` where we customized it further for this site. 

![Boutique Architecture]({{ site.baseurl }}/assets/images/boutique_architecture.png)

Procedure is as follows:

1. Sign In to [GitHub]({{site.data.urls.github}})

1. Navigate to **Import Repository** and enter the following:

    | Field | Value |
    |-------|-------|
    | Your old repository’s clone URL  | https://github.com/pangealab/cassandra.git |
    | Your new repository owner | YOUR GIT ACCOUNT | 
    | Your new repository name | Any memorable name (e.g. `cassandra`) |
    | Privacy | `Public` |