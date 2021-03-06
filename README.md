# WhatsApp Business API Setup Scripts  (English)

This repository includes all configuration scripts used to set up WhatsApp Business API using `Kubernetes Engine on Google Cloud Platform'.

Step 1. Creare custom VPC and subnet:

```gcloud compute networks create 'network_name' --project='project_name' --subnet-mode=custom --mtu=1460 --bgp-routing-mode=regional && gcloud compute networks subnets create 'subnet_name' --project=rake-'project_name' --range='IP_range' --network='network_name' --region='region'```

- Go to created VPC network 
- Allocate IP range in Private Service Connection
- Create connection in Private Connection to Services and select allocated IP range

Step 2. Create Google Kubernetes Engine with following parametres:

```gcloud beta container clusters create "test-gke-clone-1" --project "rake-system-test" --region "us-central1" --no-enable-basic-auth --cluster-version "1.21.3-gke.2003" --release-channel "regular" --machine-type "e2-medium" --image-type "COS_CONTAINERD" --disk-type "pd-ssd" --disk-size "20" --metadata disable-legacy-endpoints=true --scopes "https://www.googleapis.com/auth/devstorage.read_only","https://www.googleapis.com/auth/logging.write","https://www.googleapis.com/auth/monitoring","https://www.googleapis.com/auth/servicecontrol","https://www.googleapis.com/auth/service.management.readonly","https://www.googleapis.com/auth/trace.append" --max-pods-per-node "110" --num-nodes "3" --logging=SYSTEM,WORKLOAD --monitoring=SYSTEM --enable-private-nodes --master-ipv4-cidr "172.17.0.0/28" --enable-ip-alias --network "projects/rake-system-test/global/networks/test-vpc" --subnetwork "projects/rake-system-test/regions/us-central1/subnetworks/test-subnet" --no-enable-intra-node-visibility --default-max-pods-per-node "110" --no-enable-master-authorized-networks --addon=HorizontalPodAutoscaling --addon=HttpLoadBalancing,GcePersistentDiskCsiDriver,GceFilestoreCsiDriver --enable-autoupgrade --enable-autorepair --max-surge-upgrade 1 --max-unavailable-upgrade 0 --enable-shielded-nodes --node-locations "us-central1-a"```

Step 3. Create PostgreSQL:




For more details related to WhatsApp Business API, please visit the documentation at: https://developers.facebook.com/docs/whatsapp

## Support for this repo
This GitHub repo is not actively monitored. If you need help, please check previously asked questions in the [WA Business API Developer Community](https://developers.facebook.com/community?sort=trending&category=766772797555412) or raise a [Direct support ticket](https://developers.facebook.com/docs/whatsapp/contact-support). Meanwhile, we are happy to continue with less time-sensitive discussions in GitHub.

## License

WhatsApp Business API Setup Scripts is [MIT licensed](./LICENSE).
