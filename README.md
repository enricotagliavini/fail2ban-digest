## fail2ban-digest: email digest aggregator for fail2ban

Fail2ban can be annoying for the large volumes of emails it can send.
Disabling email sending completely can solve the annoyance, but leaves
the Admin uninformed. With fail2ban-digest you can configure a arbitrary
period digest to be send, like


	Hi,

	   this is a digest email of banned IPs since 2017-05-15 00:11:41 UTC and 2017-05-15 01:00:03

	 20 event(s) for IP 0.0.0.1                                   : 2017-05-14 03:20:54, 2017-05-14 04:03:28, 2017-05-14 04:45:03, 2017-05-14 05:27:02, 2017-05-14 06:50:40, 2017-05-14 07:18:32, 2017-05-14 08:00:38, 2017-05-14 08:43:21, 2017-05-14 09:26:09, 2017-05-14 10:22:46, 2017-05-14 10:50:49, 2017-05-14 11:32:33, 2017-05-14 12:28:12, 2017-05-14 13:38:53, 2017-05-14 14:21:42, 2017-05-14 15:04:04, 2017-05-14 15:46:40, 2017-05-14 16:43:08, 2017-05-14 17:25:12, 2017-05-14 18:07:17
	  4 event(s) for IP 0.0.0.2                                   : 2017-05-14 18:35:51, 2017-05-14 19:05:13, 2017-05-14 22:12:05, 2017-05-14 23:46:37
	  3 event(s) for IP 0.0.0.3                                   : 2017-05-14 19:43:37, 2017-05-14 21:42:28, 2017-05-15 00:52:59

	Regards,

	Fail2ban digest


The digest can also be shown on the command line by calling
	$ fail2ban_digest digest sshd
	  2 event(s) for IP 0.0.0.1                                   : 2017-05-15 06:48:35, 2017-05-15 07:06:37
	  1 event(s) for IP 0.0.0.2                                   : 2017-05-15 16:09:51

Using the digest action for command line display will not empty the database by default, while send the email digest will empty it.
This can be changed by using the `--delete` and `--no-delete` options.

Setup
-------------

Required dependencies:
- Python 3.4 or newer is required. It might work with python 3.3, but testing was with 3.4 and newer only.
- [Fail2ban](https://github.com/fail2ban/fail2ban) version 0.9 or newer

There is no setup script / build system at the moment. It might come in the future.

Manual Installation:
- Copy `config/action.d/digest.conf` in `/etc/fail2ban/action.d`
- Create a directory for the database, a common location on most Linux systems can be `/var/lib/fail2ban/digest`
- If necessary adjust the path in `bin/fail2ban_digest` script to point to the correct `db_location`
- Copy `bin/fail2ban_digest` in a system folder
- Configure the sshd jail to use the digest action as shown in the `examples/jail.local` file
- Configure a periodic cron job to send the mail digest. An example for a daily mail can be found in examples/fail2ban-digest.cron

License:
--------

Fail2Ban is free software; you can redistribute it and/or modify it under the
terms of the GNU General Public License as published by the Free Software
Foundation; either version 2 of the License, or (at your option) any later
version.

Fail2Ban is distributed in the hope that it will be useful, but WITHOUT ANY
WARRANTY; without even the implied warranty of MERCHANTABILITY or FITNESS FOR A
PARTICULAR PURPOSE. See the GNU General Public License for more details.

You should have received a copy of the GNU General Public License along with
Fail2Ban; if not, write to the Free Software Foundation, Inc., 51 Franklin
Street, Fifth Floor, Boston, MA 02110, USA

