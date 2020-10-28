

Skip to content
Using Gmail with screen readers
in:sent 
Meet
New meeting
Join a meeting
Hangouts

1 of 2,759
PHP Assignment - Mirafra
Inbox

Jyotsna Sharma
AttachmentsWed, Oct 21, 6:40 PM (7 days ago)
Hi Priyabrata, Please find the PHP assignment and complete it in 2-3 working days. Once completed please share the folder and the path. Thanks and regards, Jyot

Priyabrata Barik <priyabratacse86@gmail.com>
Attachments
Sun, Oct 25, 10:10 PM (3 days ago)
to Jyotsna

Hi Jyotsna,
I did not get time so I could not complete it.
But I did main functionality.

--
Thanks & Regards
Priyabrata
+91-9718205945
Attachments area

<?php
	$bucketName = 'SUB_YOUR_BUCKET_NAME_IN';
	$IAM_KEY = 'SUB_YOUR_IAM_KEY_IN';
	$IAM_SECRET = 'SUB_YOUR_IAM_SECRET_IN';

	// Connect to AWS
	try {
		$s3 = S3Client::factory(
			array(
				'credentials' => array(
					'key' => $IAM_KEY,
					'secret' => $IAM_SECRET
				),
				'version' => 'latest',
				'region'  => 'us-east-2'
			)
		);
	} catch (Exception $e) {
		die("Error: " . $e->getMessage());
	}

	
	$fileURL = 'SUB_IN_YOUR_IMAGE_PATH'; 
	$keyName = 'test_example/' . basename($fileURL);
	$pathInS3 = 'https://s3.us-east-2.amazonaws.com/' . $bucketName . '/' . $keyName;

	// Add it to S3
	try {
		if (!file_exists('/tmp/tmpfile')) {
			mkdir('/tmp/tmpfile');
		}
				
		$tempFilePath = '/tmp/tmpfile/' . basename($fileURL);
		$tempFile = fopen($tempFilePath, "w") or die("Error: Unable to open file.");
		$fileContents = file_get_contents($fileURL);
		$tempFile = file_put_contents($tempFilePath, $fileContents);

		$s3->putObject(
			array(
				'Bucket'=>$bucketName,
				'Key' =>  $keyName,
				'SourceFile' => $tempFilePath,
				'StorageClass' => 'REDUCED_REDUNDANCY'
			)
		);

	} catch (S3Exception $e) {
		die('Error:' . $e->getMessage());
	} catch (Exception $e) {
		die('Error:' . $e->getMessage());
	}


	echo 'Done';

?>
aws.php
Displaying aws.php.
