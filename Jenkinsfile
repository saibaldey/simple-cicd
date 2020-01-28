pipeline {
node {'master'} {
  stage{"File Upload"} {
    def inputFile = input message: 'Upload file', parameters: [file(name: 'hosts')]
    new hudson.FilePath(new File("${WORKSPACE}/hosts")).copyFrom(inputFile)
    inputFile.delete()
  }
  stage{"Check Input file"} {
    conditionCheck = fileExists('hosts')toString()
    if(conditionCheck == 'true'){
      sh '''sed -i 'li [hostgroup]' hosts'''
      echo "File Uploaded Successfully"
    }
    else{
      echo "File Upload failed"
      return
    }
  }
  stage{"Validaing OS Versions"} {
    try{
      sh "cd ${WORKSPACE} && ansible-playbook -i hosts version-check.yml --limit {{hostlist}}"
    } catch(e) {
      echo{"************ VERSION CHECK FAILED ****************"}
      throw e
    }
  }
}
}
