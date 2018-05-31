node {
    def app

    stage('Clone Repository') {
        checkout scm
    } 
    
    stage('Application security testing') {
        environment {
            analyzer.bundle.audit.enabled=false
        }   
        sh 'echo "Trying to run depedency check"'
        sh 'echo $analyzer.bundle.audit.enabled'
        dependencyCheckAnalyzer datadir: 'dependency-check-data', isFailOnErrorDisabled: true, hintsFile: '', includeCsvReports: false, includeHtmlReports: false, includeJsonReports: false, isAutoupdateDisabled: false, outdir: '', scanpath: 'package.json', skipOnScmChange: false, skipOnUpstreamChange: false, suppressionFile: '', zipExtensions: ''
        dependencyCheckPublisher canComputeNew: false, defaultEncoding: '', healthy: '', pattern: '', unHealthy: ''        
        archiveArtifacts allowEmptyArchive: true, artifacts: '**/dependency-check-report.xml', onlyIfSuccessful: true
        
/*	sh '/home/ubuntu/dependency-check/bin/dependency-check.sh --project "Juice Shop" --scan . --format HTML --disableRubygems --disableBundleAudit --disablePyPkg --disablePyDist' */
        step([$class: 'DependencyCheckPublisher', unstableTotalAll: '0'])

   }
}
