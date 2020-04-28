# mod_slotlimit
mod_slotlimit is an Apache 2.2 module that use a dynamic slot allocation algorithm and static rules in order to manage resources used for each running site avoiding RAM and CPU monopolization https://lucaercoli.it/



# Configuration options



AvailableSlotsPercent


Syntax: AvailableSlotsPercent number

Default: 0

Percentage of apache slots available in order to set any restrictions. Setting it to 0 dynamic slot allocation algorithm will be deactivated. When has remained free the specified percentage of apache slots, module start to manage incoming connections, penalizing sites that are monopolizing the resources of the server.


N.B. Before activating this option check that the apache scoreboard display correct vhost name of the running sites. In order to make this you can activate (momentarily) mod_status and connect to http://yourserver/server-status. If Vhost hostname do not display correctly the name of the sites visited sets up to "On" the directive "ForceVhostName" before using "AvailableSlotsPercent".




MaxConnectionsPerSite


Syntax: MaxConnectionsPerSite number

Default: No Limit

Max connections for each running site

N.B. Like for "AvailableSlotsPercent" if Vhost hostname do not display correctly the name of the sites visited sets up to "On" the directive "ForceVhostName".




ClientIpLimit


Syntax: ClientIpLimit number

Default: 40

Number of maximum simultaneous connection per IP.



ForceVhostName


Syntax: ForceVhostName On|Off

Default: Off

Force vhost hostname in scoreboard. Vhost hostname do not match site visited under some conditions, for example with some mass virtual hosting technique. In order to check that this is not your case you can use mod_status. Setting this directive to On, mod_slotlimit will overwrite vhost hostname in apache scoreboard.



CustomErrMsg


Syntax: CustomErrMsg "My custom error message"
Default: "Blocked by mod_slotlimit. More information about this error may be available in the server error log."

A custom error message that allows you to replace default error message with one you create



CustomLimitsFile


Syntax: CustomLimitsFile /path/to/file

Default: No Value

Using this directive you can specify limits customized for each running site, penalizing or privileged it. In the file should be stored (line by line) the site name and the number of usable slots. You can add comments by using the '#' character. The file format is as follows:


..

www.sitename1.it 10

www.site2.com 35

..




# Module config example



AvailableSlotsPercent 10

MaxConnectionsPerSite 40

ClientIpLimit 30

CustomLimitsFile /etc/apache2/mod_slotlimit.rules

ForceVhostName On


