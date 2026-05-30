---
layout: default
title: VoXtream2
permalink: /
---

<div style="text-align:center;">

  <h1>Full-stream TTS with dynamic speaking rate control via duration distribution guidance</h1>

  <!-- badges -->
  <p>
    <a href="https://anonymous.4open.science/r/voxtream2" target="_blank">
      <img src="https://img.shields.io/badge/GitHub-Code-green" />
    </a>
    <a href="https://huggingface.co/voxtream2/model" target="_blank">
      <img src="https://img.shields.io/badge/%F0%9F%A4%97%20HuggingFace-Model-yellow" />
    </a>
    <a href="https://huggingface.co/spaces/voxtream2/demo" target="_blank">
      <img src="https://img.shields.io/badge/%F0%9F%A4%97%20HuggingFace-Demo-yellow" />
    </a>
  </p>

  <!-- authors -->
  <div style="margin:1rem auto 2rem; font-size: 18px; font-style: italic;">
  Anonymous submission
  </div>

  <iframe
    src="https://www.youtube-nocookie.com/embed/hzGV28HY9qs?si=nuEIHYGL7Pw-vTKR"
    width="560"
    height="315"
    title="VoXtream2 demo"
    frameborder="0"
    allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share"
    referrerpolicy="strict-origin-when-cross-origin"
    allowfullscreen>
  </iframe>

  <!-- abstract -->
  <div style="width:85%; margin:0 auto;">
    <h2>Overview</h2>
    <p style="font-size: 16px;">
      We present VoXtream2, a zero-shot full-stream TTS model with dynamic speaking-rate control that can be updated mid-utterance on the fly.
      <ul style="font-size: 16px; text-align:left;">
          <li><b>Dynamic speed control</b>: Duration distribution guidance and Classifier-free guidance allow for a fine-grained speaking rate control, which can be adjusted as the model generates speech.</li>
          <li><b>Streaming performance</b>: Works <b>4x</b> times faster than real-time and achieves <b>74 ms</b> first packet latency in a full-stream on a consumer GPU.</li>
          <li><b>Translingual capability</b>: Prompt text masking enables support of acoustic prompts in any language.</li>
      </ul>
    </p>
  </div>

  <p style="font-size: 16px;">
  Try <a href="https://huggingface.co/spaces/voxtream2/demo" target="_blank">VoXtream2 ⚡</a> in your browser on HuggingFace 🤗 spaces.
  </p>

  <!-- architecture -->
  <img src="{{ "/assets/img/architecture_v2.svg" | relative_url }}"
     alt="Architecture"
     style="width:75%; height:auto; display:block; margin:2rem auto 2rem;" />

  <h2>Dynamic speaking-rate control</h2>

  <p style="font-size: 16px; width:85%; margin:0 auto;">
  The first row shows a gradual speed up or slowdown of speaking rate, and the second row shows how the model responds to sharp changes of the control signal.
  </p>

  <style>
  .spk-rate-demo {
    max-width: 900px;
    margin: 0 auto 3rem;
  }
  .spk-rate-audgrid {
    display: grid;
    align-items: start;
    grid-template-columns: 6% 42% 8% 42% 6%;
    width: 100%;
    margin-top: 12px;
  }
  .spk-rate-row {
    margin: 0 auto 20px auto;
    width: 100%;
  }
  .spk-rate-row img {
    width: 100%;
    height: auto;
    display: block;
  }
  .spk-rate-col {
    width: 100%;
  }
  .spk-rate-aud {
    width: 70%;
    display: block;
    margin: 0 auto;
  }
  .spk-rate-txt {
    width: 100%;
    margin: 10px 0 10px 0;
    overflow-wrap: anywhere;
    white-space: normal;
    font-size: 14px;
    line-height: 1.35;
    text-align: center;
  }
  .spk-rate-label {
    text-align: center;
    font-size: 14px;
    font-weight: bold;
    margin: 0 0 6px 0;
  }
  </style>

  <div class="spk-rate-demo">
    <div class="spk-rate-row">
      <img src="{{ "/assets/img/dynamic_spk_rate_sequential.svg" | relative_url }}" alt="Sequential speaking-rate control"/>
      <div class="spk-rate-audgrid">
        <div></div>
        <div class="spk-rate-col">
          <div class="spk-rate-label">Acoustic prompt</div>
          <audio class="spk-rate-aud" controls src="{{ "/assets/audio/spk_rate/dynamic/prompt_linear_1_7.wav" | relative_url }}"></audio>
          <div class="spk-rate-txt">Well. My commute started out normal, then it got weird. A driver saw me running, but the door stayed closed. By then I was not angry, just tired of guessing the timing. I waited next to a man giving directions to everyone. The board changed twice before I reached the stop.</div>
          <audio class="spk-rate-aud" controls src="{{ "/assets/audio/spk_rate/dynamic/linear_1_7.wav" | relative_url }}"></audio>
        </div>
        <div></div>
        <div class="spk-rate-col">
          <div class="spk-rate-label">Acoustic prompt</div>
          <audio class="spk-rate-aud" controls src="{{ "/assets/audio/spk_rate/dynamic/prompt_linear_7_1.wav" | relative_url }}"></audio>
          <div class="spk-rate-txt">Here is the thing. Tonight I made a simple meal, at least that was the plan. I tasted the soup too early and added salt too soon. I kept checking the stove like it might change by itself. Then I had to balance it out with more water. The pot looked messy at first, but it slowly came together.</div>
          <audio class="spk-rate-aud" controls src="{{ "/assets/audio/spk_rate/dynamic/linear_7_1.wav" | relative_url }}"></audio>
        </div>
        <div></div>
      </div>
    </div>

    <div class="spk-rate-row">
      <img src="{{ "/assets/img/dynamic_spk_rate_interleave.svg" | relative_url }}" alt="Interleaved speaking-rate control"/>
      <div class="spk-rate-audgrid">
        <div></div>
        <div class="spk-rate-col">
          <div class="spk-rate-label">Acoustic prompt</div>
          <audio class="spk-rate-aud" controls src="{{ "/assets/audio/spk_rate/dynamic/prompt_interleave_1_7.wav" | relative_url }}"></audio>
          <div class="spk-rate-txt">Okay, so. The meeting started on time and ended nowhere near on time. One person shared a screen with too many tabs open. Then we spent twenty minutes arguing about names for files. Everyone had a different version of what was agreed.</div>
          <audio class="spk-rate-aud" controls src="{{ "/assets/audio/spk_rate/dynamic/interleave_1_7.wav" | relative_url }}"></audio>
        </div>
        <div></div>
        <div class="spk-rate-col">
          <div class="spk-rate-label">Acoustic prompt</div>
          <audio class="spk-rate-aud" controls src="{{ "/assets/audio/spk_rate/dynamic/prompt_interleave_7_1.wav" | relative_url }}"></audio>
          <div class="spk-rate-txt">All right, so. We both liked the movie, but we did not agree on why. I cared about the pacing and my friend cared about the music. It was more about how it felt than what actually happened. The funny part is that we agreed on the ending the whole time.</div>
          <audio class="spk-rate-aud" controls src="{{ "/assets/audio/spk_rate/dynamic/interleave_7_1.wav" | relative_url }}"></audio>
        </div>
        <div></div>
      </div>
    </div>
  </div>
  
  <!-- non stream audio -->
  <h2>Static speaking-rate control</h2>

  <style>
  .spk-static-rate-table {
    border-collapse:collapse;
    width:100%;
    table-layout:fixed;
    margin:0 auto;
    white-space:normal;
  }
  .spk-static-rate-table .static-aud {
    width:180px;
  }
  </style>

  <div style="
       width:100%;
       overflow-x:auto;
       -webkit-overflow-scrolling:touch;
       margin:0.75rem 0 2rem;">

  <table class="spk-static-rate-table">
    <colgroup>
      <col style="width: 15%;">
      <col style="width: 20%;">
      <col style="width: 15%;">
      <col style="width: 15%;">
      <col style="width: 15%;">
    </colgroup>
    <thead>
        <tr style="border-bottom:3px solid currentColor;">
            <th style="vertical-align : middle;text-align: center">Speech Prompt</th>
            <th style="vertical-align : middle;text-align: center">Text</th>
            <th style="vertical-align : middle;text-align: center">VoiceStar</th>
            <th style="vertical-align : middle;text-align: center">MaskGCT</th>
            <th style="vertical-align : middle;text-align: center">VoXtream2</th>
        </tr>
    </thead>
    <tbody>
    <tr>
        <td style="vertical-align : middle;text-align:center;border:0;">
          <div class="spk-rate-label">Slow ➔ Fast</div>
          <audio class="static-aud" controls="controls"><source src="{{ "/assets/audio/spk_rate/static/slow_male.wav" | relative_url }}" autoplay="">Your browser does not support the audio element.</audio><br>
        </td>
        <td style="vertical-align: middle; height: 100px; border:0; overflow-wrap: break-word; white-space: normal;">Look, I took the wrong bus once, and it dropped me two stops late, so I walked the rest of the way, and I found a small cafe, that had decent tea.</td>
        <td style="vertical-align : middle;text-align:center;border:0;"><audio class="static-aud" controls="controls"><source src="{{ "/assets/audio/spk_rate/static/slow_fast_voicestar.wav" | relative_url }}" autoplay="">Your browser does not support the audio element.</audio><br> </td>
        <td style="vertical-align : middle;text-align:center;border:0;"><audio class="static-aud" controls="controls"><source src="{{ "/assets/audio/spk_rate/static/slow_fast_maskgct.wav" | relative_url }}" autoplay="">Your browser does not support the audio element.</audio><br> </td>
        <td style="vertical-align : middle;text-align:center;border:0;"><audio class="static-aud" controls="controls"><source src="{{ "/assets/audio/spk_rate/static/slow_fast_voxtream2.wav" | relative_url }}" autoplay="">Your browser does not support the audio element.</audio><br> </td>
    </tr>
    <tr>
        <td style="vertical-align : middle;text-align:center;border:0;">
          <div class="spk-rate-label">Fast ➔ Slow</div>
          <audio class="static-aud" controls="controls"><source src="{{ "/assets/audio/spk_rate/static/fast_female.wav" | relative_url }}" autoplay="">Your browser does not support the audio element.</audio><br>
        </td>
        <td style="vertical-align: middle; height: 100px; border:0; overflow-wrap: break-word; white-space: normal;">So, my cat stared at the door, like it heard something outside, so I opened the window, and it just sniffed the air, then walked away.</td>
        <td style="vertical-align : middle;text-align:center;border:0;"><audio class="static-aud" controls="controls"><source src="{{ "/assets/audio/spk_rate/static/fast_slow_voicestar.wav" | relative_url }}" autoplay="">Your browser does not support the audio element.</audio><br> </td>
        <td style="vertical-align : middle;text-align:center;border:0;"><audio class="static-aud" controls="controls"><source src="{{ "/assets/audio/spk_rate/static/fast_slow_maskgct.wav" | relative_url }}" autoplay="">Your browser does not support the audio element.</audio><br> </td>
        <td style="vertical-align : middle;text-align:center;border:0;"><audio class="static-aud" controls="controls"><source src="{{ "/assets/audio/spk_rate/static/fast_slow_voxtream2.wav" | relative_url }}" autoplay="">Your browser does not support the audio element.</audio><br> </td>
    </tr>
    <tr>
        <td style="vertical-align : middle;text-align:center;border:0;">
          <div class="spk-rate-label">Normal ➔ Fast</div>
          <audio class="static-aud" controls="controls"><source src="{{ "/assets/audio/spk_rate/static/normal_female.wav" | relative_url }}" autoplay="">Your browser does not support the audio element.</audio><br>
        </td>
        <td style="vertical-align: middle; height: 100px; border:0; overflow-wrap: break-word; white-space: normal;">Okay, so my brother called me at 7, he sounded tired, but he still joked around, and it made me laugh, even though my day was messy, and I was glad.</td>
        <td style="vertical-align : middle;text-align:center;border:0;"><audio class="static-aud" controls="controls"><source src="{{ "/assets/audio/spk_rate/static/normal_fast_voicestar.wav" | relative_url }}" autoplay="">Your browser does not support the audio element.</audio><br> </td>
        <td style="vertical-align : middle;text-align:center;border:0;"><audio class="static-aud" controls="controls"><source src="{{ "/assets/audio/spk_rate/static/normal_fast_maskgct.wav" | relative_url }}" autoplay="">Your browser does not support the audio element.</audio><br> </td>
        <td style="vertical-align : middle;text-align:center;border:0;"><audio class="static-aud" controls="controls"><source src="{{ "/assets/audio/spk_rate/static/normal_fast_voxtream2.wav" | relative_url }}" autoplay="">Your browser does not support the audio element.</audio><br> </td>
    </tr>
    <tr>
        <td style="vertical-align : middle;text-align:center;border:0;">
          <div class="spk-rate-label">Normal ➔ Slow</div>
          <audio class="static-aud" controls="controls"><source src="{{ "/assets/audio/spk_rate/static/normal_male.wav" | relative_url }}" autoplay="">Your browser does not support the audio element.</audio><br>
        </td>
        <td style="vertical-align: middle; height: 100px; border:0; overflow-wrap: break-word; white-space: normal;">Right, my cat stared at the door, like it heard something outside, so I opened the window, and it just sniffed the air, then walked away, and it felt worth it.</td>
        <td style="vertical-align : middle;text-align:center;border:0;"><audio class="static-aud" controls="controls"><source src="{{ "/assets/audio/spk_rate/static/normal_slow_voicestar.wav" | relative_url }}" autoplay="">Your browser does not support the audio element.</audio><br> </td>
        <td style="vertical-align : middle;text-align:center;border:0;"><audio class="static-aud" controls="controls"><source src="{{ "/assets/audio/spk_rate/static/normal_slow_maskgct.wav" | relative_url }}" autoplay="">Your browser does not support the audio element.</audio><br> </td>
        <td style="vertical-align : middle;text-align:center;border:0;"><audio class="static-aud" controls="controls"><source src="{{ "/assets/audio/spk_rate/static/normal_slow_voxtream2.wav" | relative_url }}" autoplay="">Your browser does not support the audio element.</audio><br> </td>
    </tr>
    </tbody>
  </table>
  </div>
  
  <!-- stream audio -->
  <h2>Translingual voice cloning</h2>

  <p style="font-size: 16px;">
  Prompt text masking allows for translingual (any language to English) voice cloning.
  </p>

  <div style="
       width:100%;
       overflow-x:auto;
       -webkit-overflow-scrolling:touch;
       margin:0.75rem 0;">

  <table style="
           border-collapse:collapse;
           width:auto;                /* don't shrink to container */
           margin:0 auto;             /* keep centered when not scrolling */
           table-layout:auto;
           white-space:nowrap;">
    <thead>
        <tr style="border-bottom:3px solid currentColor;">
            <th style="vertical-align : middle;text-align: center">Language</th>
            <th style="vertical-align : middle;text-align: center">Speech Prompt</th>
            <th style="vertical-align : middle;text-align: center">Text</th>
            <th style="vertical-align : middle;text-align: center">VoXtream2</th>
        </tr>
    </thead>
    <tbody>
    <tr>
        <td style="font-size: 15px;border:0;">Chinese</td>
        <td style="vertical-align : middle;text-align:center;border:0;"><audio controls="controls" style="width: 200px;"><source src="{{ "/assets/audio/translingual/chinese_female.wav" | relative_url }}" autoplay="">Your browser does not support the audio element.</audio><br> </td>
        <td style="vertical-align: middle; height: 100px;border:0; overflow-wrap: break-word; white-space: normal;">VoXtream2 combines a distribution matching mechanism over duration states with classifier-free guidance across conditioning signals to improve controllability and synthesis quality.</td>
        <td style="vertical-align : middle;text-align:center;border:0;"><audio controls="controls" style="width: 200px;"><source src="{{ "/assets/audio/translingual/chinese_female_voxtream2.wav" | relative_url }}" autoplay="">Your browser does not support the audio element.</audio><br> </td>
    </tr>
    <tr>
        <td style="font-size: 15px;border:0;">Hindi</td>
        <td style="vertical-align : middle;text-align:center;border:0;"><audio controls="controls" style="width: 200px;"><source src="{{ "/assets/audio/translingual/hindi_male.wav" | relative_url }}" autoplay="">Your browser does not support the audio element.</audio><br> </td>
        <td style="vertical-align: middle; height: 100px;border:0; overflow-wrap: break-word; white-space: normal;">Prompt-text masking enables textless audio prompting, removing the need for prompt transcription.</td>
        <td style="vertical-align : middle;text-align:center;border:0;"><audio controls="controls" style="width: 200px;"><source src="{{ "/assets/audio/translingual/hindi_male_voxtream2.wav" | relative_url }}" autoplay="">Your browser does not support the audio element.</audio><br> </td>
    </tr>
    <tr>
        <td style="font-size: 15px;border:0;">Spanish</td>
        <td style="vertical-align : middle;text-align:center;border:0;"><audio controls="controls" style="width: 200px;"><source src="{{ "/assets/audio/translingual/spanish_male.wav" | relative_url }}" autoplay="">Your browser does not support the audio element.</audio><br> </td>
        <td style="vertical-align: middle; height: 100px;border:0; overflow-wrap: break-word; white-space: normal;">Across standard zero-shot benchmarks and a dedicated speaking-rate test set, VoXtream2 achieves competitive objective and subjective results against public baselines.</td>
        <td style="vertical-align : middle;text-align:center;border:0;"><audio controls="controls" style="width: 200px;"><source src="{{ "/assets/audio/translingual/spanish_male_voxtream2.wav" | relative_url }}" autoplay="">Your browser does not support the audio element.</audio><br> </td>
    </tr>
    <tr>
        <td style="font-size: 15px;border:0;">Arabic</td>
        <td style="vertical-align : middle;text-align:center;border:0;"><audio controls="controls" style="width: 200px;"><source src="{{ "/assets/audio/translingual/arabic_female.wav" | relative_url }}" autoplay="">Your browser does not support the audio element.</audio><br> </td>
        <td style="vertical-align: middle; height: 100px;border:0; overflow-wrap: break-word; white-space: normal;">In full-stream mode, it runs 4 times faster than real time with 74 ms first-packet latency on a consumer GPU.</td>
        <td style="vertical-align : middle;text-align:center;border:0;"><audio controls="controls" style="width: 200px;"><source src="{{ "/assets/audio/translingual/arabic_female_voxtream2.wav" | relative_url }}" autoplay="">Your browser does not support the audio element.</audio><br> </td>
    </tr>
    <tr>
        <td style="font-size: 15px;border:0;">French</td>
        <td style="vertical-align : middle;text-align:center;border:0;"><audio controls="controls" style="width: 200px;"><source src="{{ "/assets/audio/translingual/french_female.wav" | relative_url }}" autoplay="">Your browser does not support the audio element.</audio><br> </td>
        <td style="vertical-align: middle; height: 100px;border:0; overflow-wrap: break-word; white-space: normal;">It has long been argued that conversational agents must be able to generate speech incrementally.</td>
        <td style="vertical-align : middle;text-align:center;border:0;"><audio controls="controls" style="width: 200px;"><source src="{{ "/assets/audio/translingual/french_female_voxtream2.wav" | relative_url }}" autoplay="">Your browser does not support the audio element.</audio><br> </td>
    </tr>
    <tr>
        <td style="font-size: 15px;border:0;">Russian</td>
        <td style="vertical-align : middle;text-align:center;border:0;"><audio controls="controls" style="width: 200px;"><source src="{{ "/assets/audio/translingual/russian_female.wav" | relative_url }}" autoplay="">Your browser does not support the audio element.</audio><br> </td>
        <td style="vertical-align: middle; height: 100px;border:0; overflow-wrap: break-word; white-space: normal;">Recent progress in neural text-to-speech (TTS) synthesis has led to highly natural and intelligible speech generation.</td>
        <td style="vertical-align : middle;text-align:center;border:0;"><audio controls="controls" style="width: 200px;"><source src="{{ "/assets/audio/translingual/russian_female_voxtream2.wav" | relative_url }}" autoplay="">Your browser does not support the audio element.</audio><br> </td>
    </tr>
    <tr>
        <td style="font-size: 15px;border:0;">Swedish</td>
        <td style="vertical-align : middle;text-align:center;border:0;"><audio controls="controls" style="width: 200px;"><source src="{{ "/assets/audio/translingual/swedish_male.wav" | relative_url }}" autoplay="">Your browser does not support the audio element.</audio><br> </td>
        <td style="vertical-align: middle; height: 100px;border:0; overflow-wrap: break-word; white-space: normal;">However, most contemporary systems implicitly assume that speaking rate is static across an utterance, typically allowing only coarse, global control over speed.</td>
        <td style="vertical-align : middle;text-align:center;border:0;"><audio controls="controls" style="width: 200px;"><source src="{{ "/assets/audio/translingual/swedish_male_voxtream2.wav" | relative_url }}" autoplay="">Your browser does not support the audio element.</audio><br> </td>
    </tr>
    </tbody>
  </table>

</div>
