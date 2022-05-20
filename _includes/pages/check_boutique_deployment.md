### Check Boutique Deployment

After all 12 Boutique Pods have been deployed, you should check all the pod statuses. In addition, retrieve and safeguard the `frontend-external` service EXTERNAL-IP for your demos. Procedure is as follows:

1. Start a Bash Shell

{% include pages/login_to_aks.md %}

1. Retrieve the `frontend-external` service EXTERNAL-IP

    ```
    kubectl get service frontend-external -n cassandra
    ```

1. Browse to the EXTERNAL-IP to view the Boutique Application

    ![Boutique Frontend](/images/boutique_frontend.png)