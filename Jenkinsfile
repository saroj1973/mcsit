pipeline {
 agent any
	environment{
		NETLIFY_SITE_ID = '6a2041a7-b4f0-4fa4-a148-45daacfce086'
		NETLIFY_AUTH_TOKEN = credentials('netlify-token')
	}

   stages {
        stage('Build') {
            agent {
                docker {
                    image 'node:18-alpine'
                    reuseNode true
                }
            }
            steps {
                sh '''
                    ls -la
                    node --version
                    npm --version
                    npm ci
                    npm run build
                    ls -la
                '''
            }
        }
stage('Deploy') {
            agent {
                docker {
                    image 'node:18-alpine'
                    reuseNode true
                }
            }
            steps {
                sh '''
                	npm install netlify-cli
                	node_modules/.bin/netlify --version
                	node_modules/.bin/netlify status
		    	node_modules/.bin/netlify deploy –-dir/=build --prod
		    '''
            }
}


    }
}
