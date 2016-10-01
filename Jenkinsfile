stage 'Input'
    def result = input message: 'Write me some input?', ok: 'Yes', parameters: [[$class: 'StringParameterDefinition', defaultValue: 'Test', description: 'Write something', name: 'Test']]

stage 'Do it'
    echo "Input was ${result}"

stage 'Who did it'
    echo "Approved by ${getLatestApprover()}"

@NonCPS
def getLatestApprover() {
   def latest = null

   // this returns a CopyOnWriteArrayList, safe for iteration
   def acts = currentBuild.rawBuild.getAllActions()
   for (act in acts) {
       if (act instanceof org.jenkinsci.plugins.workflow.support.steps.input.ApproverAction) {
           latest = act.userId
       }
   }
   return latest
}
