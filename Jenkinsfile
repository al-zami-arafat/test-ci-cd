pipeline {
    agent any

      stages {
          stage('build') {
              steps {
                  echo 'building the software'
                //   sh 'npm install'
              }
          }
          stage('test') {
              steps {
                  echo 'testing the software'
                //   sh 'npm test'
              }
          }

          stage('deploy') {
              steps {
                withCredentials([sshUserPrivateKey(credentialsId: "jenkins-ssh", keyFileVariable: 'sshkey')]){
                  echo 'deploying the software'
                  sh '''#!/bin/bash
                  echo "Creating .ssh"
                  mkdir -p /var/lib/jenkins/.ssh
                  ssh-keyscan 192.168.33.11 >> /var/lib/jenkins/.ssh/known_hosts
                  ssh-keyscan 192.168.33.12 >> /var/lib/jenkins/.ssh/known_hosts

                  rsync -avz --exclude  '.git' --delete -e "ssh -i $sshkey" ./ vagrant@192.168.33.11:/app/
                  rsync -avz --exclude  '.git' --delete -e "ssh -i $sshkey" ./ vagrant@192.168.33.12:/app/

                  ssh -i $sshkey vagrant@192.168.33.11 "sudo systemctl restart nodeapp"
                  ssh -i $sshkey vagrant@192.168.33.12 "sudo systemctl restart nodeapp"

                  '''
              }
          }
      }
    }
}




// pipeline {
//     agent any
//     stages {
//         stage('Build') {
//             steps {
//                 sh 'echo "Hello World"'
//                 sh '''
//                     echo "Multiline shell steps works too"
//                     ls -lah
//                 '''
//             }
//         }
//     }
// }




// // pipeline {
// //     agent any
// //     environment{
// //         staging_server="23.111.182.242"
// //     }
// //     stages {
// //         stage('git repo & clean') {
// //             steps {
// //                 bat "git clone https://github.com/al-zami-arafat/test-ci-cd.git"
// //             }
// //         }
// //         stage('install') {
// //             steps {
// //                 bat "mvn install -f test-ci-cd"
// //             }
// //         }
// //         stage('test') {
// //             steps {
// //                 bat "mvn test -f test-ci-cd"
// //             }
// //         }
// //         stage('package') {
// //             steps {
// //                 bat "mvn package -f test-ci-cd"
// //             }
// //         }
// //     }
// // }


// pipeline{
//     agent any
//     environment{
//         staging_server="103.214.22.75"
//     }
//     stages{
//         stage('Deploy to Remote'){
//             steps{
//                 sh '''
//                     for fileName in `find ${WORKSPACE} -type f -mmin -10 | grep -v ".git" | grep -v "Jenkinsfile"`
//                     do
//                         fil=$(echo ${fileName} | sed 's/'"${JOB_NAME}"'/ /' | awk {'print $2'})
//                         scp -r ${WORKSPACE}${fil} root@${staging_server}:/www/wwwroot/jenkins-test.giveawork.com${fil}
//                     done
//                 '''
//             }
//         }
//     }
// }