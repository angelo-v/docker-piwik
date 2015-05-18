aveltens/piwik
=========

This image may be used to restore a piwik instance from a backup.

[How do I backup Piwik data and files?](http://piwik.org/faq/how-to-install/faq_138/)

Example docker-compose.yml to run a piwik container linked to a mysql database container:

    mysql:
      image: mysql
      expose:
       - 3306
      env_file:
       - ./mysql.env
    piwik:
      image: aveltens/piwik
      ports:
        - "80:80"
      links:
        - mysql
      volumes:
        - backups:/backups
        
The backups folder must contain a backup of your config.ini.php and mysql database in the following form:

 - config.ini.php.20150815
 - backup_20150815.sql.bz2
 
20150815 is a timestamp in the format yyyyMMdd.
 
After starting the containers, restore the backup via the following command:

`docker exec <piwik-container-name> restore 20150815`

You may create additional backups using the following command:

`docker exec <piwik-container-name> backup`

(Only one backup per day. If you run it again the backup files from that day will be overwritten.)
 
## License

The MIT License (MIT)

Copyright (c) 2015, Angelo Veltens

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in
all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN
THE SOFTWARE.


