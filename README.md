# Metaforce
Metaforce is a Ruby gem for interacting with the [Salesforce Metadata API](http://www.salesforce.com/us/developer/docs/api_meta/index.htm).
The goal of this project is to make the [Migration Tool](http://www.salesforce.com/us/developer/docs/apexcode/Content/apex_deploying_ant.htm) obsolete, favoring Rake over Ant.

## Usage
``` ruby
client = Metaforce::Metadata::Client.new :username => 'username',
    :password => 'password',
    :security_token => 'security token')

client.describe
# => { :metadata_objects => [{ :child_xml_names => "CustomLabel", :directory_name => "labels" ... }

client.list(:type => "CustomObject")
# => [{ :created_by_id => "005U0000000EGpcIAG", :created_by_name => "Eric Holmes", ... }]

deployment = client.deploy(File.expand_path("../src"))
# => #<Metaforce::Transaction:0x00000102779bf8 @id="04sU0000000WNWoIAO" @type=:deploy> 

deployment.done?
# => false

deployment.result(:wait_until_done => true)
# => { :id => "04sU0000000WNWoIAO", :messages => [{ :changed => true ... :success => true }
```

## License
one line to give the program's name and an idea of what it does.
Copyright (C) yyyy  name of author

This program is free software; you can redistribute it and/or
modify it under the terms of the GNU General Public License
as published by the Free Software Foundation; either version 2
of the License, or (at your option) any later version.

This program is distributed in the hope that it will be useful,
but WITHOUT ANY WARRANTY; without even the implied warranty of
MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
GNU General Public License for more details.

You should have received a copy of the GNU General Public License
along with this program; if not, write to the Free Software
Foundation, Inc., 51 Franklin Street, Fifth Floor, Boston, MA  02110-1301, USA.
