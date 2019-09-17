node {

	def lib = library (
		identifier: 'simple-lib@master', 
		retriever: 
			modernSCM([
				$class: 'GitSCMSource', 
				credentialsId: 'sshkeygithub', 
				id: 'sshkeygithub', 
				remote: 'git@github.com:kobemtl/test1.git', 
				traits: [[$class: 'jenkins.plugins.git.traits.BranchDiscoveryTrait']]
			])
	)
    stage("Checkout class"){
        lib.by.bulgak.jenkins.lib.Checkout.new().checkout(
            "git@github.com:kobemtl/test1.git",
            "master"
        );
    }

    stage("Maven builder"){
        def mavenLib = lib.by.bulgak.jenkins.lib
        def mvn = mavenLib.Maven.builder(this)
            .action("clean install")
            .argument(mavenLib.MavenArgument.create().withPrefix("-D").withKey("key").withName("value").build())
            .argument(mavenLib.MavenArgument.create().withPrefix("-D").withKey("key2").withName("value2").build())
            .silent(true)
            .build();
       def constants = mavenLib.Constants.new()
        mvn.execute(constants.MAVEN);
    }
}