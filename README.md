# jipsterious_help
Vebosed the commands.

1. SSH into Synology NAS - 'ssh <admin user>@NAS IP or hostname e.g. ssh admin@nas'.

2. Sudo to root user 'sudo -i'.

3. Go to directory 'cd /usr/syno/etc.defaults'.

4. Run your favourite text editor and update scemd.xml file 'vi scemd.xml'.
Editors available in Synology: vi, vim.  Personally, I'm used to vi so I use that.

Scroll down the file and look for fan speeds.
DUAL_MODE_HIGH is for the "cool mode" (i.e., when Synology keeps things cooler at the expense of noise)
DUAL_MODE_LOW = "quiet mode"
I've updated the "low mode" only, like this:

<?xml version="1.0" encoding="UTF-8"?>
        <adt_fan_config skip_check_temp="10" type="DUAL_MODE_LOW" hibernation_speed="UNKNOWN">
                <alert_config threshold="2" period="30" alert_temp="95" shutdown_temp="100" name="cpu"/>
                <alert_config threshold="2" period="300" alert_temp="58" shutdown_temp="61" name="disk"/>
                <alert_config threshold="2" period="30" alert_temp="68" shutdown_temp="71" name="m2"/>
                <alert_config threshold="2" period="30" alert_temp="95" shutdown_temp="100" name="nic"/>
                <pwm_config name="pwm2" pwm_duty_high="255" pwm_duty_low="80" high_freq="yes" sensor_type="manual"/>
                <fan_mapping_config name="internal" pwm="pwm2" order="0"/>
                <fan_mapping_config name="internal" pwm="pwm2" order="1"/>
                <fan_mapping_config name="internal" pwm="pwm2" order="2"/>

                <manual_config name="cpu_temperature" threshold="2" period="30" temp="0" fan_speed="30"/>
                <manual_config name="cpu_temperature" threshold="2" period="30" temp="66" fan_speed="100"/>
                <manual_config name="cpu_temperature" threshold="2" period="30" temp="76" fan_speed="150"/>
                <manual_config name="cpu_temperature" threshold="2" period="30" temp="84" fan_speed="200"/>
                <manual_config name="cpu_temperature" threshold="2" period="30" temp="90" fan_speed="255"/>

                <manual_config name="disk_temperature" threshold="2" period="300" temp="0" fan_speed="30"/>
                <manual_config name="disk_temperature" threshold="2" period="300" temp="47" fan_speed="100"/>
                <manual_config name="disk_temperature" threshold="2" period="300" temp="52" fan_speed="150"/>
                <manual_config name="disk_temperature" threshold="2" period="300" temp="56" fan_speed="200"/>
                <manual_config name="disk_temperature" threshold="2" period="300" temp="58" fan_speed="255"/>

                <manual_config name="m2_temperature" threshold="2" period="30" temp="0" fan_speed="30"/>
                <manual_config name="m2_temperature" threshold="2" period="30" temp="57" fan_speed="100"/>
                <manual_config name="m2_temperature" threshold="2" period="30" temp="62" fan_speed="150"/>
                <manual_config name="m2_temperature" threshold="2" period="30" temp="65" fan_speed="200"/>
                <manual_config name="m2_temperature" threshold="2" period="30" temp="68" fan_speed="255"/>

                <manual_config name="nic_temperature" threshold="2" period="30" temp="0" fan_speed="30"/>
                <manual_config name="nic_temperature" threshold="2" period="30" temp="78" fan_speed="150"/>
                <manual_config name="nic_temperature" threshold="2" period="30" temp="86" fan_speed="200"/>
                <manual_config name="nic_temperature" threshold="2" period="30" temp="92" fan_speed="255"/>
   <!-- Etc. -->
</scemd>

2. Restart the scemd service

From the SSH session:
systemctl restart scemd
