# Delete Cloud Foundry Deployment and Release, BOSH Deployment#

This document explains how to delete a Cloud Foundry Deployment and BOSH Deployment.

##Deleting the Cloud Foundry Deployment and Release##

+ Go to the cloudfoundry deployment directory.

  `cd /home/user/cloudfoundry/deployments`

+ Execute command: `bosh deployments`

   Output of the above command is similar to the listing below:


          $ bosh deployments

            +--------------+--------------+-------------------------------+
            | Name         | Release(s)   | Stemcell(s)                   |
            +--------------+--------------+-------------------------------+
            | cloudfoundry | appcloud/119 | bosh-vsphere-esxi-ubuntu/1029 |
            +--------------+--------------+-------------------------------+

+ Run the following command to delete the Cloud Foundry deployment:

  `bosh delete deployment cloudfoundry`

  Output of the above command is partially listed below:

           $bosh delete deployment cloudfoundry

           You are going to delete deployment `cloudfoundry'.

           THIS IS A VERY DESTRUCTIVE OPERATION AND IT CANNOT BE UNDONE!

           Are you sure? (type 'yes' to continue): yes

           Director task 42

           Deleting instances


+ Once Cloud Foundry is deleted, the next step is to delete the Cloud Foundry release. You can get the release name as follows:

  `bosh releases`

   Output of the above command is similar to the listing below. Cloud Foundry's release name uploaded to BOSH is appcloud.

          $ bosh releases

            +----------+-----------+
            | Name     | Versions  |
            +----------+-----------+
            | appcloud | 106, 119* |
            +----------+-----------+
            (*) Currently deployed

            Releases total: 1

+ Execute the following command to delete the Cloud Foundry release:

 `bosh delete release appcloud`

   Output of the above command is partially listed below:

          $ bosh delete release appcloud
            Deleting `appcloud'
            Are you sure? (type 'yes' to continue): yes

            Director task 43

            Deleting packages

This completes the deletion of a Cloud Foundry release from BOSH.

## Delete BOSH Deployment

+ First delete the BOSH stemcell as follows


 `bosh delete stemcell bosh-vsphere-esxi-ubuntu 1029`
You can find the stemcell name from the output of `bosh deployment` which we executed above.

   Output of the above command is partially listed below:

          $ bosh delete stemcell bosh-vsphere-esxi-ubuntu 1029
            Checking if stemcell exists...
            You are going to delete stemcell `bosh-vsphere-esxi-ubuntu/1029'
            Are you sure? (type 'yes' to continue): yes

            Director task 44

            Deleting stemcell from cloud

+ Once stemcell is deleted,the deployment target should be set to Micro BOSH.

+ Now BOSH Deployment can be deleted.

+ Execute following command to get the name of BOSH deployment:

 `bosh deployments`

   Output of the above command is similar to listing below:

        $ bosh deployments

          +------+------------+-------------------------------+
          | Name | Release(s) | Stemcell(s)                   |
          +------+------------+-------------------------------+
          | bosh | bosh/10    | bosh-vsphere-esxi-ubuntu/1029 |
          +------+------------+-------------------------------+

          Deployments total: 1

+ Execute following command to delete the BOSH deployment:

 `bosh delete deployment bosh`

Output of the above command is partially listed below:

        $bosh delete deployment bosh

         You are going to delete deployment `bosh'.

         THIS IS A VERY DESTRUCTIVE OPERATION AND IT CANNOT BE UNDONE!

         Are you sure? (type 'yes' to continue): yes

         Director task 6

         Deleting instances

 This deletes the BOSH deployment from Micro BOSH.
