### jenkinsnote
## Reset Jenkins Admin Credentails
# 1) Path to check default jenkins admin credenatils 
/var/lib/jenkins/secrets/initialAdminPassword

# 2) Path to check jenkins root configuration
/var/lib/jenkins/config.xml

# 3) If you forgot admin credentails and want to reset 
Stop Jenkins
Go go edit /var/lib/jenkins/config.xml
Change <useSecurity>true</useSecurity> to false
Restart Jenkins: sudo service jenkins restart
Navigate to the Jenkins dashboard to the "Configure Security" option you likely used before. This time, setup security the same as before, BUT set it to allow anyone to do anything, and allow user signup.

