pipeline {
    agent any

    parameters {
        string(name: 'p_base_dir', defaultValue: '/scmlocal/de.kleiber.demos.oracle.database.tdd/target/generated-docs', description: 'base directory to mount in decktape container')
        string(name: 'p_presentation', defaultValue: '/home/user/reveal/presentation.html', description: 'presentation dir/file or url')
        choice(name: 'p_fragments', choices: ['false', 'true'], description: 'print one per page fragment instead the page as a whole')
        string(name: 'p_slides', defaultValue: '1-66', description: 'presentation dir/file or url')
        choice(name: 'p_size', choices: ['1920x1080'], description: 'target size of the presentation')
    }

    stages {
        stage('Build') {
            steps {
                sh "docker run --rm -t -v `pwd`:/slides -v ${params.p_base_dir}:/home/user astefanutti/decktape ${params.p_presentation}?fragments=${params.p_fragments} presentation.pdf --slides ${params.p_slides} --size ${params.p_size}"
                // sh 'docker run --rm -t -v `pwd`:/slides -v /scmlocal/de.kleiber.demos.oracle.database.tdd/target/generated-docs:/home/user astefanutti/decktape /home/user/reveal/presentation.html?fragments=false presentation.pdf --slides 1 --size 1920x1080'
                archiveArtifacts 'presentation.pdf'
            }
        }
    }
}