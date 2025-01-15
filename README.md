This folder contains client tools to be used in the context of HE applied to the health use-case of ENCRYPT (oncology).
- SetUpBinInDocker : allows to generate the cryptographic parameters and key, and then to encrypt the initial database.
- GetResultBinInDocker : allows to decrypt the output from the analytics.

Here is how the whole workflow is ran :

A- CRYPTOGRAPHIC SETUP/ DATA ENCRYPTION (SetUpBinInDocker)
1) put the clear database table.csv inside the data subfolder of SetUpBinInDocker
2) docker build, then docker run (with the option -it)
3) run the binary file inside the container (./encrypt-medical-setup)
4) the output files are inside the result folder inside the container.

B- HE ANALYSIS (through the ENCRYPT platform)
run the health HE analytics through the ENCRYPT platform (./stats-hom-eval), the inputs being:
- a request request.csv ;
- all the files outputted by the SetUp tool of step A, EXCEPT THE SECRET KEY key-private.txt.

C- RESULT DECRYPTION (GetResultInDocker)
1) put the inputs inside the data subfolder of GetResultBinInDocker:
- the files cryptocontext.txt and key-private.txt outputted by the SetUp tool of step A ;
- the output from the analytic component at step B, named as "encrypted_result.txt".
2) docker build, then docker run (with the option -it)
3) run the binary file inside the container (./encrypt-medical-getresult)
4) the output file is inside the result folder inside the container.
