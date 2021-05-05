<script>
  import Player from './Player.svelte'
</script>

<style>
  #outstream-container {
    width: 500px;
    margin: 0 auto;
  }
</style>

<div id="outstream-container">
  <Player
    aspectRatio="16:9"
    customParam1="customParam1"
    customParam2="customParam2"
    customParam3="customParam3"
    videoUrl="https://assets.connatix.com/Elements/a2b4e744-6884-4300-8eeb-a4394fe485d4/Disney-Vast.xml"
    videoType="vast"
    cnxPlayerId="f77f1ffc-2602-45e7-a41e-68e65b9bd20b"
    cnxLineItemId="e642cb74-0713-44f1-b858-8348ae737abb"
  />
</div>