pipeline{
      // 定义本次构建使用哪个标签的构建环境，本示例中为 “slave-pipeline”
      agent{
        node{
          label 'slave-pipeline'
        }
      }

      // "stages"定义项目构建的多个模块，可以添加多个 “stage”， 可以多个 “stage” 串行或者并行执行
      stages{
        // 定义第一个stage， 完成克隆源码的任务, 示例项目中包含用于本次构建的编排文件Jenkinsfile 和 应用部署文件deployment.yaml
        stage('Git'){
          steps{
            git branch: 'master', credentialsId: '', url: 'https://github.com/haoshuwei/ack-jenkins-demo-pipeline.git'
          }
        }

        // 添加第二个stage, 部署应用到Kubernetes集群
        stage('Deploy'){
          steps{
              container("kubectl") {
                  sh "kubectl apply -f deployment.yaml"
              }
          }
        }

      }
    }
