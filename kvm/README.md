# InsightAgent: kvm
Agent Type: kvm

Platform: Linux

InsightFinder agent can be used to monitor system performance metrics for the host and all the guests on a KVM enabled machine.

##### Instructions to register a project in Insightfinder.com
- Go to [insightfinder.com](https://insightfinder.com/)
- Sign in with the user credentials or sign up for a new account.
- Go to Settings and Register for a project under "Insight Agent" tab.
- Give a project name, select Project Type as "Private Cloud".
- View your account information by clicking on your user id at the top right corner of the webpage. Note the license key number.

##### Pre-requisites:
Python 2.7.

Python 2.7 must be installed in order to launch deployInsightAgent.sh. For Debian and Ubuntu, the following command will ensure that the required dependencies are present

Libvirt should be installed on the system. The download link can be found here:
https://libvirt.org/

Also, the python package libvirt-python should be installed on the system. We have tested with the version 1.3.1. You can follow the link to download and install libvirt-python.
https://pypi.python.org/pypi/libvirt-python

```
sudo apt-get upgrade
sudo apt-get install build-essential libssl-dev libffi-dev python-dev wget
```
For Fedora and RHEL-derivatives
```
sudo yum update
sudo yum install gcc libffi-devel python-devel openssl-devel wget
```

##### To install agent on local machine
1) Use the following command to download the insightfinder agent code.
```
wget --no-check-certificate https://github.com/insightfinder/InsightAgent/archive/master.tar.gz -O insightagent.tar.gz
```
Untar using this command.
```
tar -xvf insightagent.tar.gz
```

2) In InsightAgent-master directory, run the following commands to install and use python virtual environment for insightfinder agent:
```
./deployment/checkpackages.sh -env
```
```
source pyenv/bin/activate
```

3) Run the below command to install agent. The -w parameter can be used to give server url example ***-w http://192.168.78.85:8080***  in case you have an on-prem installation otherwise it is not required. The SAMPLING_INTERVAL and REPORTING_INTERVAL vaules support 10 second granularity along with minute granularity. Minute granularity can be set with a single integer whereas the 10 second granularity is set by using the value **10s**. e.g. **-s 10s -r 2**
```
./deployment/install.sh -i PROJECT_NAME -u USER_NAME -k LICENSE_KEY -s SAMPLING_INTERVAL -r REPORTING_INTERVAL -t AGENT_TYPE
```
AGENT_TYPE = kvm
After using the agent, use command "deactivate" to get out of python virtual environment.

NOTE: To install packages locally to the virtual environment, use pip install -I <package-name>. That way pip will install the package locally even though a system-wide version exists.
