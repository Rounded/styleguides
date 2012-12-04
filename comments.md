# Commenting and Headers Logs

## Header Logs
After any major changes are made to a file, please place a log of the date, your initials, and a quick summary of what you did in the head. 
If possible, the logs should be made server-side. The logs should be descriptive of major changes only and optionally provide links to relevant resources.

	  BAD
	  ```ruby
	  # 7/26/12 BW - Added a comma to the second sentence.
	  ```
	  GOOD
	  ```ruby
	  # 7/26/12 BW - CURL requests now use Facebook Open Graph API to pull Fanpage feeds. http://developers.facebook.com
	  
	  

## Comments should:
1. Explain the code in "non-code" terms, and (if possible) what it's accomplishing in the grand scheme of things

	  BAD
	  ```ruby
	  # get each user as u and set u.password to md5
	  User.each do |u|
	  	u.password = Digest::MD5.new()
	  end
	```
	  GOOD
	  ```ruby
	  # In case we get hacked, this will generate an MD5 hash for all users passwords in the database
	  User.each do |u|
	  	u.password = Digest::MD5.new()
	  end
	```
2. Be well formatted, in plain english, and consistent

	  BAD
	  ```ruby
	  # geet each users As u...
	  User.each do |u|
	  	u.password = Digest::MD5.new() # set u.password too randum md5
	  end
	```
	  GOOD
	  ```ruby
	  # We are iterating through each user in the database
	  User.each do |u|
	  	# We are generating an MD5 hash for their password
	  	u.password = Digest::MD5.new()
	  end
	```

3. Explain what the code is doing. But, only when its non-obvious / needed for clarification.

	  BAD
	  ```ruby
	  # get all the paid users
	  paid_users = User.paid
	  ```
	  GOOD
	  ```ruby
	  paid_users = User.paid
	```

4. Assume that the reader is a technical person
5. Attempt to refractor your code in a way that will make comments unncecessary

	BAD
	```ruby
	# This will find the first fish in the barrel sorted by age
	jigglypuff = Fish.all.sort_by { |x| x.age }
	```
	GOOD
	```ruby
	youngest_fish = Fish.all.sort_by { |f| f.age }

## Comments should NOT:
1. Explain functions or methods that are part of the language and or framework
2. Be lengthy or cumbersome to read.