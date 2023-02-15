Before you start - search how to untaint the master role to allow our workload to run on the master also .

1. Create an NGINX Daemonset
   - Make sure it only runs on instances with label:
     - type=external_facing

2. Create the following application Mockup
   - Create a deployment for spring-music:latest 
     - Make sure it only runs on:
       1. Where node label = type=external_facing
       2. Where NGINX pods exists
     - Use antipod affinity to allow only a SINGLE springapp to run on each machine.

3. Create an Elasticsearch - not using daemonset
   - Elastic is partitioned  so we need to make sure that each pod of ES will work only on machines that are not tainted and has only a single ES instance on it.
