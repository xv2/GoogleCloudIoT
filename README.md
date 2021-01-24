Original tutorial: https://cloud.google.com/community/tutorials/cloud-iot-gateways-rpi

Repository `git clone https://github.com/GoogleCloudPlatform/community.git`


### Create virtual machine
* Download and install `ubuntu-20.04.1-desktop-amd64.iso`

### Steps:

* step by step for `console.cloud.google.com` in original tutorial

#### Steps in VirtualMachine:

* `sudo apt install net-tools`
* `sudo apt install python3`
* `sudo apt install python3-pip`
* `sudo apt install build-essential libssl-dev libffi-dev python3-dev`
* `apt-get install python3-venv`
* `git clone git@github.com:xv2/GoogleCloudIoT.git`
* `cd GoogleCloudIoT/cloud-iot-gateways-rpi`
* if needed regenerate your rsa keys `./generate_keys.sh` and set public key in your gateway authentication in Google Cloud IoT Console
* set valid region if needed `--cloud_region=us-central1` in `./run-gateway` at line 20, also check `--registry_id`, `--gateway_id` and your can temporary set `--project_id` instead of use `export GOOGLE_CLOUD_PROJECT=your-project-id-123`
* `wget https://pki.goog/roots.pem`
* `pip3 install virtualenv`
* `python3 -m venv venv`
* `python3 -m virtualenv venv`
* `source venv/bin/activate`
* `pip install -r requirements-pi.txt`
* `pip install -r requirements-gateway.txt`


##### Run gateway
* open new terminal window `./cloud-iot-gateways-rpi`
* `source venv/bin/activate`
* `source run-gateway`

##### Run run-led-light
* open new terminal window `./cloud-iot-gateways-rpi`
* `source venv/bin/activate`
* `source run-led-light`
* you can `UPDATE CONFIG` in cloud console for your device (set `ON` or `OFF` configuration value and see result in ubuntu terminal)

:tada: **My congratulations you can use Google Cloud IoT!**


### NOTICES
if your have error `on_disconnect 1: Out of memory.` you need create Cloud Pub/Sub topics and bind it to registry

Sample error logs:
```
$ source run-gateway
Creating JWT using RS256 from private key file rsa_private.pem
on_publish, userdata None, mid 1
Unable to find key 1
connect status False
on_connect Connection Accepted.
on_disconnect 1: Out of memory.
```
