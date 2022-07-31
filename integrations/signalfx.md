<center><h1> Signalfx </center>

<br>
SignalFX
<br>
                SignalFX uses SignalFlow programming language to learn how to create charts and decectors using program_text.

<br>
Provider
    <br>
                Terraform uses providers to connect configurations to the system
 
<br>
Example Provider:
                
                terraform {
                                required_providers {
                                                signalfx = {
                                                                source = "splunk-terraform/signalfx"
                                                                version = "6.14.0"
                                                }
                                }
                }
 
                provider "signalfx" {
                                auth_token = "${var.signalfx_auth_token}"
                                #API URL Realm
                                #api_url = https://api.us2.signalfx.com
                                #Custom URL
                                #custom_app_url = https://myorg.signalfx.com
                }
 
 
 
<br>
Authentication

<li>SignalFX API uses either Org Tokens or Session Tokens. Session Tokens are short-lived and expire quickly while Org Tokens have longer duration.</li>
<br>
Detector
<li>Creates and Manages features such as Historical Anomaly, Resource Running Out and others using the SignalFlow programming language.</li>
<br>
<br> 
Arguments Required for Detector:

                Name - Name of Detector
                Program_Text - SignalFlow Program Text for the Detector
                Rule - Set of Rules for the Alerting
                Detect_Label - Detect Label which matches a detect label within program_text
                Severity - Must be one of the following: "Critical", "Major", "Minor", "Warning", "Info"
                Label - Used in the publish statement that displays the plot metric time series data




<br>
 
Example Detector:

                resource "signalfx_detector" "Delay" {
                                count = length(var.clusters)

                                name = " max average delay - ${var.clusters[count.index]}"
                                max_delay = 30

                                program_text = <<-EOF
                                                signal = data('app.delay', filter('cluster', ${var.clusters[count.index]}))
                                                detect(when(signal > 60, '5m')).publish('Processing old messages 5m')
                                                detect(when(signal > 60, '30m')).publish('Processing old messages 30m')
                                EOF

                                rule {
                                                description = "Max > 60 for 30m"
                                                severity = "Critical"
                                                detect_lavel = "Processing old messages 30m"
                                                notifications = ["Email, Ops@scrippshealth.org"]
                                }
                }

                provider "signalfx" {}

                variable "clusters" {
                                default = ["clusterA","clusterB"]
                }

SignalFX Teams
Handles the management of teams

Arguments required for Teams
Name

Optional Arguments
Description - Description of the team
Members - List of User IDs to include in the team
notifications_critical - Where to send critical alerts
notifications_default - Where to send default alerts
notifications_major - Where to send major alerts
notifications_minor - Where to send minor alerts
notifications_warning - Where to send warning alerts
notifications_info - Where to send informational alerts

Example Teams Resource:

                resource "signalfx_team" "TeamNameHere" {
                                name = "Team Name Here"

                                members = [
                                                "user1",
                                                "user2",
                                                #...
                                ]

                                notifications_default = [
                                                "Email, Ops@scrippshealth.org"
                                ]
                }

SignalFX Dashboard
Curated collection of specific charts and supported filters, variables and time range options. These options allow for drill down for more details on the data.
SignalFX Dashboard Group
Collection of dashboards

Example Dashboard Resource

                resource "signalfx_dashboard" "MyDashBoard1" {
                                name = "My Dashboard"
                                dashboard_group = signalfx_dashboard_group.mydashboardgroup1.id

                                time_range = "-30m"

                                filter {
                                                property = "collector"
                                                values = ["cpu", "Diamond"]
                                }

                                variable {
                                                property = "region"
                                                alias = "region"
                                                values = ["uswest-1-"]
                                }

                                chart {
                                                chart_id = signalfx_time_chart.mychart1.id
                                                width = 12
                                                height = 1
                                }


                                chart {
                                                chart_id = signalfx_time_chart.mychart2.id
                                                width = 12
                                                height = 1
                                }
                }

Example Dashboard Permissions

                resource "signalfx_dashboard" "MyDashBoard1_ACL" {
                                name = "My Dashboard1"
                                dashboard_group = signalfx_dashboard_group.mydashboardgroup1.id

                                permissions {
                                                acl {
                                                                principal_id = "abc123"
                                                                principal_type = "ORG"
                                                                actions = ["READ"]
                                                }
                                                acl {
                                                                principal_id = "xyz987"
                                                                principal_type = "USER"
                                                                actions = ["READ", "Write"]
                                                }
                                }
                }
