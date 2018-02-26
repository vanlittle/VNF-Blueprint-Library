############################################################################
##
# Copyright 2017-2018 VMware Inc.
# This file is part of VNF-ONboarding
# All Rights Reserved.
#
# Licensed under the Apache License, Version 2.0 (the "License"); you may
# not use this file except in compliance with the License. You may obtain
# a copy of the License at
#
#         http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS, WITHOUT
# WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied. See the
# License for the specific language governing permissions and limitations
# under the License.
#
# For those usages not covered by the Apache License, Version 2.0 please
# contact:  osslegalrouting@vmware.com
 
##
 
#############################################################################




VNF onboarding with Cloudify
============================

Zip structure:
/types - needed types for Standard TOSCA blueprints
/scripts - scripts used in configuration
OpenStack-inputs.yaml - inputs needed for Cloudify blueprint deployment, should be copied and filled outside the zip file 
-OpenStack.yaml - Cloudify blueprint
-OpenStack-TOSCA.yaml - Standard TOSCA blueprint
-OpenStack-OSM.yaml - Standard TOSCA blueprint


Run your VNF with Cloudify and follow steps below.

1. Setup Cloudify virtualenv.
   
    You can skip this step if your virtualenv is already created and just activate it or use Cloudify UI instead.
    
    Using virtualenv:
    `virtualenv cloudify`
    `source cloudify/bin/activate`
    
    or using virtualenv wrapper:
    `mkvirtualenv cloudify`
    
    install cloudify cli:
    `pip install cloudify==3.4.1`
    
    Use cloudify manager:
    `cfy use -t <cfy manager ip>`

2. Install
    Fill inputs template with relevant data: OpenStack-inputs.yaml
    
    At once:
    `cfy install -l -OpenStack.zip  -n -OpenStack.yaml -b  --include-logs -i OpenStack-inputs.yaml`
    
    or step by step:
    `cfy blueprints publish-archive -l -OpenStack.zip  -n -OpenStack.yaml -b -OpenStack`
    `cfy deployments create -d -OpenStack -b -OpenStack`
    `cfy executions -w install -d -OpenStack --include-logs`

3. How to operate:

    Using UI or CLI. <information>
   
4. Uninstall 

    At once:
    `cfy uninstall -d -OpenStack --include-logs`
    
    or step by step:
    `cfy executions -w uninstall -d -OpenStack`
    `cfy deployments delete -d -OpenStack`
    `cfy blueprints delete -b -OpenStack`


Standard TOSCA blueprint
------------------------

1. Setup environment
   `virtualenv env`
   `. env/bin/activate`
   `pip install git+http://git-wip-us.apache.org/repos/asf/incubator-ariatosca.git`

2. Unzip blueprints package
   `unzip -OpenStack`

3. Parse blueprint to generate model
   `aria parse -OpenStack/-OpenStack-TOSCA.yaml instance`
# VNF-Onboarding