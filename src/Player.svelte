<script>
  import { onMount } from 'svelte';
  export let aspectRatio;
  export let customParam1;
  export let customParam2;
  export let customParam3;
  export let videoUrl;
  export let cnxPlayerId;
  export let cnxLineItemId;
  export let videoType = 'hls'; // hls/vast
  
  const cnxDomId = `cnx-script-ref`;
  let singleLineItem = {
    id: cnxLineItemId,
    cpm: 2,
    priority: 'Top'
  };

  if(videoType === 'vast') {
    singleLineItem['url'] = videoUrl;
  } else {
    singleLineItem['externalHlsFile'] = videoUrl;
  }

  const [ratioWidth, ratioHeight] = aspectRatio.split(':');
  
  onMount(() => {
    cnx.cmd.push(() => {
      cnx({
        playbackMode: cnx.configEnums.PlaybackModeEnum.AutoPlay,
        nextVideoMode: cnx.configEnums.NextVideoModeEnum.Loop,
        customParam1: `${customParam1}`,
        customParam2: `${customParam2}`,
        customParam3: `${customParam3}`,
        playerId: cnxPlayerId,
        settings: {
          outstreamAdAsContent: true,
          pauseAdWhenFinished: false,
          outstreamSettings: {
            endAdBreakPolicy: cnx.configEnums.EndAdBreakPolicyEnum.Loop
          },
          advertising: {
            blockConnatixDemand: true,
            midRollOnlyOnLongContent: false,
            lineItems: [singleLineItem]
          },
          customization: {
            responsive: true,
            ratioWidth, 
            ratioHeight
          },
          outstreamSettings: {
            houseScreenColor: '#000'
          }
        }
      }).render(cnxDomId, (error, playerApi) => {
        if (error) {
          console.log('Render Error:', error);
        }
      });
    });
  });
</script>
<svelte:head>
  <script>
    !function(n) {
      if (!window.cnx) {
        window.cnx = {}, window.cnx.cmd = [];
        var t = n.createElement("iframe");
        t.display = "none", t.onload = function() {
          var n = t.contentWindow.document,
            c = n.createElement("script");
            c.src = "//cd.connatix.com/connatix.player.js", c.setAttribute("async", "1"), c.setAttribute("type", "text/javascript"), n.body.appendChild(c)
        }, n.head.appendChild(t)
      }
    }(document);
  </script>
</svelte:head>

<div id="{cnxDomId}"></div>