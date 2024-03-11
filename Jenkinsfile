// pipeline {
//     agent any
//     environment{
//         staging_server="23.111.182.242"
//     }
//     stages {
//         stage('git repo & clean') {
//             steps {
//                 bat "git clone https://github.com/al-zami-arafat/test-ci-cd.git"
//             }
//         }
//         stage('install') {
//             steps {
//                 bat "mvn install -f test-ci-cd"
//             }
//         }
//         stage('test') {
//             steps {
//                 bat "mvn test -f test-ci-cd"
//             }
//         }
//         stage('package') {
//             steps {
//                 bat "mvn package -f test-ci-cd"
//             }
//         }
//     }
// }


pipeline{
    agent any
    environment{
        staging_server="103.214.22.75"
    }
    stages{
        stage('Deploy to Remote'){
            steps{
                sh '''
                    for fileName in `find ${WORKSPACE} -type f -mmin -10 | grep -v ".git" | grep -v "Jenkinsfile"`
                    do
                        fil=$(echo ${fileName} | sed 's/'"${JOB_NAME}"'/ /' | awk {'print $2'})
                        scp -r ${WORKSPACE}{fil} root@${staging_server}:/www/wwwroot/jenkins-test.giveawork.com${fil}
                    done
                '''
            }
        }
    }
}