pipeline {
    agent any
    tools {
        maven "Maven 3.8.4"
        jdk "JDK 8 Update 221"
    }
    stages {
        stage('チェックアウト') {
            steps {
                // Gitリポジトリの指定
                git url: 'https://github.com/braccho/Jenkins_Practical_Guide_3rd_Edition.git'
            }
        }
        stage('Mavenビルド') {
            steps {
                sh "mvn clean package"
            }
        }
        stage('テスト結果の集計') {
            steps {
                // JUnit
                junit('target/surefire-reports/*.xml')
                // Jacoco
                jacoco(execPattern: 'target/jacoco.exec')
            }
        }
        stage('定義済みのジョブ呼び出し') {
            steps {
                build job: 'MultiBuild', parameters: [string(name: 'MESSAGE', value: params.PERSON)]
            }
        }
    }
}