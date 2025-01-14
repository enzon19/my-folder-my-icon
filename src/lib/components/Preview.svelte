<script>
  import { onMount } from 'svelte';

  let { colors = {}, image = {}, size = "24rem" } = $props();
  let layer0Color1 = $derived(colors.layer0Color1);
  let layer2Color1 = $derived(colors.layer2Color1);
  let layer2Color2 = $derived(colors.layer2Color2);
  let layer3Color1 = $derived(colors.layer3Color1);
  let layer3Color2 = $derived(colors.layer3Color2);
  let layer4Color1 = $derived(colors.layer4Color1);
  let layer4Color2 = $derived(colors.layer4Color2);

  let canvas;
  $inspect(image);

  $effect(renderPreviewOnCanvas); 
  function renderPreviewOnCanvas () {
    const folderSvg = `
    <svg version="1.1" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" x="0px" y="0px"
	 viewBox="0 0 256 256" style="enable-background:new 0 0 256 256;" xml:space="preserve" id="folderIcon">
  <style type="text/css">
    .st1{fill-rule:evenodd;clip-rule:evenodd;fill:url(#SVGID_1_);filter:url(#Adobe_OpacityMaskFilter);}
    .st2{mask:url(#mask0_501_11930_00000081649918554152100850000016654729337992308386_);}
    .st3{fill-rule:evenodd;clip-rule:evenodd;fill:#A6A1A1;}
    .st4{fill-rule:evenodd;clip-rule:evenodd;fill:url(#SVGID_2_);}
    .st5{fill-rule:evenodd;clip-rule:evenodd;fill:url(#SVGID_3_);}
    .st6{fill-rule:evenodd;clip-rule:evenodd;fill:url(#SVGID_4_);}
  </style>
  <path style="fill-rule:evenodd;clip-rule:evenodd;fill:${layer0Color1};" d="M104.4,42.4c-4.4-5.3-10.9-8.4-17.8-8.4H29c-6.6,0-12,5.4-12,12v12.1v10.1V160c0,6.6,5.4,12,12,12h200
    c6.6,0,12-5.4,12-12V70.1c0-6.6-5.4-12-12-12H117.4L104.4,42.4z"/>
  <defs>
    <filter id="Adobe_OpacityMaskFilter" filterUnits="userSpaceOnUse" x="17" y="62" width="224" height="110">
      <feColorMatrix  type="matrix" values="1 0 0 0 0  0 1 0 0 0  0 0 1 0 0  0 0 0 1 0"/>
    </filter>
  </defs>
  <mask maskUnits="userSpaceOnUse" x="17" y="62" width="224" height="110" id="mask0_501_11930_00000081649918554152100850000016654729337992308386_">
    
      <linearGradient id="SVGID_1_" gradientUnits="userSpaceOnUse" x1="32.5816" y1="239.5494" x2="213.3495" y2="58.4074" gradientTransform="matrix(1 0 0 -1 0 258)">
      <stop  offset="0" style="stop-color:#05815D"/>
      <stop  offset="1" style="stop-color:#0C575F"/>
    </linearGradient>
    <path class="st1" d="M104.4,42.4c-4.4-5.3-10.9-8.4-17.8-8.4H29c-6.6,0-12,5.4-12,12v12.1v10.1V160c0,6.6,5.4,12,12,12h200
      c6.6,0,12-5.4,12-12V70.1c0-6.6-5.4-12-12-12H117.4L104.4,42.4z"/>
  </mask>
  <g class="st2">
    <g>
      <path class="st3" d="M92.8,74c5,0,9.8-1.6,13.8-4.6l9.9-7.4H229c6.6,0,12,5.4,12,12v34v52c0,6.6-5.4,12-12,12H29
        c-6.6,0-12-5.4-12-12v-52V86c0-6.6,5.4-12,12-12h58H92.8z"/>
    </g>
  </g>
  <linearGradient id="SVGID_2_" gradientUnits="userSpaceOnUse" x1="17" y1="196" x2="241" y2="48" gradientTransform="matrix(1 0 0 -1 0 258)">
    <stop  offset="0" style="stop-color:${layer2Color1}"/>
    <stop  offset="0.9531" style="stop-color:${layer2Color2}"/>
  </linearGradient>
  <path class="st4" d="M92.8,74c5,0,9.8-1.6,13.8-4.6l9.9-7.4H229c6.6,0,12,5.4,12,12v34v90c0,6.6-5.4,12-12,12H29
    c-6.6,0-12-5.4-12-12v-90V86c0-6.6,5.4-12,12-12h58H92.8z"/>
  <linearGradient id="SVGID_3_" gradientUnits="userSpaceOnUse" x1="16.9254" y1="57.3174" x2="240.9429" y2="54.8172" gradientTransform="matrix(1 0 0 -1 0 258)">
    <stop  offset="0" style="stop-color:${layer4Color1}"/>
    <stop  offset="1" style="stop-color:${layer4Color2}"/>
  </linearGradient>
  <path class="st5" d="M17,194v4c0,6.6,5.4,12,12,12h200c6.6,0,12-5.4,12-12v-4c0,6.6-5.4,12-12,12H29C22.4,206,17,200.6,17,194z"/>
  <linearGradient id="SVGID_4_" gradientUnits="userSpaceOnUse" x1="17" y1="182" x2="241" y2="182" gradientTransform="matrix(1 0 0 -1 0 258)">
    <stop  offset="0" style="stop-color:${layer3Color1}"/>
    <stop  offset="1" style="stop-color:${layer3Color2}"/>
  </linearGradient>
  <path class="st6" d="M106.6,69.4c-4,3-8.8,4.6-13.8,4.6H87H29c-6.6,0-12,5.4-12,12v4c0-6.6,5.4-12,12-12h58h5.8
    c5,0,9.8-1.6,13.8-4.6l9.9-7.4H229c6.6,0,12,5.4,12,12v-4c0-6.6-5.4-12-12-12H116.5L106.6,69.4z"/>
</svg>`;
    const ctx = canvas.getContext('2d');

    // SVG
    const folderSvgBlob = new Blob([folderSvg], { type: 'image/svg+xml' });
    const folderSvgUrl = URL.createObjectURL(folderSvgBlob);

    const folderSvgImg = new Image();
    folderSvgImg.onload = () => {
      ctx.clearRect(0, 0, canvas.width, canvas.height); // Clear previous drawing
      ctx.drawImage(folderSvgImg, 0, 0);
      URL.revokeObjectURL(folderSvgUrl); // Free up memory

      // Image
      if (image.url) {
        console.log(image.url)

        const imageImg = new Image();
        imageImg.onload = () => {
          ctx.drawImage(imageImg, image.positionX, image.positionY, image.sizeWidth, image.sizeHeight);
        };
        imageImg.src = image.url;
      }
    };
    folderSvgImg.src = folderSvgUrl;
  };
</script>

<canvas bind:this={canvas} id="preview" width="1000" height="1000" class="w-full h-full"></canvas>