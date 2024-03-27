<template>
  <div class="container">
    <div>
      <h1>ARTech Leaks Challenge</h1>
      <h2>Background</h2>
      <p>
        The famous gaming company ARTech Industries has a new game coming out called Pongchamps that has everyone holding their breath in anticipation for what could possibly be the game of the year. 
        After a rival gaming company fell victim to a ransom attack not too long ago, the CEO of ARTech put out a video claiming that hackers would never be able to pull this off on them because of their advanced cybersecurity practices and procedures put in place. 
        The CEO also claimed that the company employees are top-notch and would never be so foolish to fall for a phishing scam or the like. He then makes an outrageous promise in that he will give one million dollars to whoever successfully manages to leak Pongchamps, with a guarantee that it will never happen. 
        People around the world took this as a challenge to see if they could leak Pongchamps and get that easy million. 
        However, over the coming weeks, nobody has been able to hack in and leak Pongchamps. 
        It seemed for a moment that maybe it truly was impossible…
      </p>
      <p>
        …And then your team entered the game, and you have something the others didn't: conversation receipts from internal employee conversations on their messaging platform Microsoft Teams. 
        This security breach wasn't even ARTech's fault -- Microsoft Teams messed up a security configuration and didn't notice for an hour, and your team took full advantage and retrieved as many private message threads as possible. 
        Afterwards, your team made a website to easily parse through the conversations in the hopes that there is enough information here that you can finally figure out a way to leak Pongchamps and win that prize money.
      </p>
      <h2>Assignment</h2>
      <p>
        Your team's task is simple -- leak Pongchamps and win that (hypothetical) million-dollar cash prize! 
        I want to see the most recent version of the Pongchamps source code in its entirety submitted to Blackboard.
      </p>
      <h2>Tips</h2>
      <p>Treat this like one large puzzle. You can do it!!!</p>
      <p>Keep in mind that you may need to Google things or look up information to go alongside what you read in the conversations.</p>
      <p>I highly recommend that you go through each conversation one by one, extract out any important information, and then attempt to bring it all together afterwards.</p>
      <h2>Submission</h2>
      <p>Please submit the most recent version of the Pongchamps source code to Blackboard. You may submit it as a .zip file.</p>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Home'
}
</script>

<style scoped>
.container {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  width: 40rem;
  margin-left: auto;
  margin-right: auto;
  margin-bottom: 1rem;
}
</style>