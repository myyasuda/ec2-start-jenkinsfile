node('aws-cli') {
   stage 'Start Instance.'
   sh "aws ec2 start-instances --instance-ids ${EC2_INSTANCE_ID} --profile ${AWS_PROFILE}"
   sh "aws ec2 wait instance-status-ok --instance-ids ${EC2_INSTANCE_ID} --profile ${AWS_PROFILE}"

   stage 'Get public ip address.'
   def publicIpAddress = sh(
       script: "aws ec2 describe-instances --instance-ids ${EC2_INSTANCE_ID} --profile ${AWS_PROFILE} --query 'Reservations[0].Instances[0].PublicIpAddress'",
       returnStdout: true).trim().replaceAll(/"/,"")

   stage 'Sending Mail.'
   mail (to: "${MAIL_TO}",
         subject: "${MAIL_SUBJECT}",
         body: "${MAIL_BODY}".replaceAll(/publicIpAddress/, publicIpAddress)
    );
}