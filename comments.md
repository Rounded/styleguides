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


## Comments should NOT:
1. Explain functions or methods that are part of the language and or framework
2. Be lengthy or cumbersome to read.