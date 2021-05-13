# Identity verification

The code pertaining to identity verification can be found in [idv.py](https://github.com/projectpai/paipass/blob/main/backend/identity_verification/idv.py).

Identity verification is done through Amazon's SNS, SES, and S3.

As you probably guessed, we use SES to send a verification link to the user's email. When the user clicks the link, the user is considered verified.
 
 We use SNS to send the user a text containing a randomly generated sequence of numbers. If the user enters it correctly, the user's phone number is considered verified.
 
 We use S3 for government ID verification. In this case, a sequence of random words is generated and the user is asked to record themselves, holding their government issued id while saying those randomly generated words. An admin is able to review the video and determine whether they said those words and if the ID is clear and valid. If an admin approves the verification request, the user is considered to have a verified government ID.
 
 
  