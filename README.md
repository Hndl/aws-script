# aws-script
Step0:
  install aws cli.
Step1:
  create folder in $HOME called '.aws'.
  
Step2:
  add a file called 'config'.
  my file contains the following. 
  
  [default]
  region=eu-west-1
  output=json
  [profile london]
  output = json
  region = eu-west-2
  
  region stipulates which is your pref' region and the output determines which output 
  you prefer when exec aws cli.  My preference is json.  To assist with the searching and parsing of this data, I created an node 
  app called aws-response-parser
Step3:
  [default]
  aws_access_key_id=<your access id here>
  aws_secret_access_key= <your secret key here>

  [london]
  aws_access_key_id = <your access id here>
  aws_secret_access_key = <your secret key here>
  
  
==============================================
you should be ready to use aws cli now.
example command aws lightsail get-instances 
==============================================

=============================================================================
=============================================================================
=============================================================================

file: aws-response-parser
description: makes it easy to scan aws cli response using a JSON output for data.  Auto detects json objects on stdin...

examples: check for existance of a server: aws lighsail get-instances --profile london | node aws-response-parser "lon-svrnode-nCache.01"
returns: name:lon-svrnode-nCache.01,state:16,statename:running,prvtIPAddr:17n.2n.n.nnn,pubIPAddr:nn.nnn.nnn.nnnn

find a staic ip asset which is not attached to a server in london region.
examples: aws lightsail get-static-ips --profile london | node aws-response-parser "lon" --free-static-ip

=============================================================================
=============================================================================
=============================================================================
=============================================================================

file: aws.ls.createinstance
#	Process Flow:
#		1: Create Instance [free/cheap instance of server]
#			a: Linux, Git, Node, Hndle/nCache
#		2: Wait until instance is running
#			a: check instance created
#		3: Restrict Ports
#			a: SSH:22
#			b: nCache: 5000-50001
#		4: Check for Free Static IP
#			a: if unattached static IP exists, then attach it.
#			b: if requested, create static ip
#				1: attach it to instance.
#		
#
Notes: 
  1:uses the 'london' profile.  to use default amend ${PRO_FILE} in the script.
  2:dependent on the aws-response-parser 
  3:dependent on nodejs.
  
example cmd line: aws.ls.createinstance lon nCache.01

