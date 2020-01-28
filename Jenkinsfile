node {"master"} {
  stage{"Validaing OS Versions"} {
    try{
      sh "cd ${WORKSPACE} && ansible-playbook -i hosts version-check.yml --limit ${hostlist}"
    } catch(e) {
      echo{"************ VERSION CHECK FAILED ****************"}
      throw e
    }
  }
}
