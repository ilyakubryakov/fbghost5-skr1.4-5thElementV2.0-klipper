pipeline {
    agent rpi-home
    options {
        ansiColor('xterm')
    }
    stages {
        stage('Commit Changes'){
        steps {
            task('Commit all files with Klipper configs'){
                sh("""
                cd /home/k3lmiir/klipper_config
                git add . 
                git commit -m "Updated `date`"
                """)
            }
        }
        }
        stage('Commit Approval'){
        steps {
            script{
            def userInput = input(id: 'confirm', message: 'Apple changes to github?', parameters [$class 'BooleanParameterDefinition', defaultValue: false, description: 'Apply changes?', name: 'confirm'])
        }
        }
        }
        stage('Push Changes'){
            steps{
                task('Push changes to the github'){
                sh("""
                eval $(ssh-agent)
                ssh-add ~/.ssh/github.prv
                git push
                """)
                }
            }
        } 
}