#Pwn

廖子慶  
2016/12/13 <!-- .element: align="right" -->

---

## Pwn ->  
## pwn2own ->
## Penetration to own
運行的程式存在漏洞  
透過漏洞取得權限

--

# 可pwn

* Web Server
* FTP
* OS
* Browser
* Player
* Texteditor

Any application

--

# pwn的方法

* Format string
* Stack overflow
* Heap exploit
* Racecondition

--

# 為了防止被pwn

* DEP
* ASLR
* UAC

But... 

---

# CTF裡的pwn

提供Network IO, binary  
連線cat flag

```shell
nc pwn.ctf.com 5566
```

--

# SOP

<svg height="599.76953125" version="1.1" width="100%" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" style="background-color: white; overflow: hidden; position: relative; left: -0.5px; top: -0.59375px;" viewBox="0 0 1193.20703125 599.76953125" preserveAspectRatio="xMidYMid meet">
    <desc style="-webkit-tap-highlight-color: rgba(0, 0, 0, 0);">Created with Raphaël 2.2.0</desc>
    <defs style="-webkit-tap-highlight-color: rgba(0, 0, 0, 0);">
        <path stroke-linecap="round" d="M5,0 0,2.5 5,5z" id="raphael-marker-block" style="-webkit-tap-highlight-color: rgba(0, 0, 0, 0);"></path>
        <marker id="raphael-marker-endblock33-obj7zr63" markerHeight="3" markerWidth="3" orient="auto" refX="1.5" refY="1.5" style="-webkit-tap-highlight-color: rgba(0, 0, 0, 0);">
            <use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#raphael-marker-block" transform="rotate(180 1.5 1.5) scale(0.6,0.6)" stroke-width="1.6667" fill="black" stroke="none" style="-webkit-tap-highlight-color: rgba(0, 0, 0, 0);"></use>
        </marker>
        <marker id="raphael-marker-endblock33-objcsbyd" markerHeight="3" markerWidth="3" orient="auto" refX="1.5" refY="1.5" style="-webkit-tap-highlight-color: rgba(0, 0, 0, 0);">
            <use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#raphael-marker-block" transform="rotate(180 1.5 1.5) scale(0.6,0.6)" stroke-width="1.6667" fill="black" stroke="none" style="-webkit-tap-highlight-color: rgba(0, 0, 0, 0);"></use>
        </marker>
        <marker id="raphael-marker-endblock33-objyv21f" markerHeight="3" markerWidth="3" orient="auto" refX="1.5" refY="1.5" style="-webkit-tap-highlight-color: rgba(0, 0, 0, 0);">
            <use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#raphael-marker-block" transform="rotate(180 1.5 1.5) scale(0.6,0.6)" stroke-width="1.6667" fill="black" stroke="none" style="-webkit-tap-highlight-color: rgba(0, 0, 0, 0);"></use>
        </marker>
        <marker id="raphael-marker-endblock33-objff9q1" markerHeight="3" markerWidth="3" orient="auto" refX="1.5" refY="1.5" style="-webkit-tap-highlight-color: rgba(0, 0, 0, 0);">
            <use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#raphael-marker-block" transform="rotate(180 1.5 1.5) scale(0.6,0.6)" stroke-width="1.6667" fill="black" stroke="none" style="-webkit-tap-highlight-color: rgba(0, 0, 0, 0);"></use>
        </marker>
        <marker id="raphael-marker-endblock33-objbp56f" markerHeight="3" markerWidth="3" orient="auto" refX="1.5" refY="1.5" style="-webkit-tap-highlight-color: rgba(0, 0, 0, 0);">
            <use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#raphael-marker-block" transform="rotate(180 1.5 1.5) scale(0.6,0.6)" stroke-width="1.6667" fill="black" stroke="none" style="-webkit-tap-highlight-color: rgba(0, 0, 0, 0);"></use>
        </marker>
        <marker id="raphael-marker-endblock33-objfgo63" markerHeight="3" markerWidth="3" orient="auto" refX="1.5" refY="1.5" style="-webkit-tap-highlight-color: rgba(0, 0, 0, 0);">
            <use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#raphael-marker-block" transform="rotate(180 1.5 1.5) scale(0.6,0.6)" stroke-width="1.6667" fill="black" stroke="none" style="-webkit-tap-highlight-color: rgba(0, 0, 0, 0);"></use>
        </marker>
        <marker id="raphael-marker-endblock33-obj540te" markerHeight="3" markerWidth="3" orient="auto" refX="1.5" refY="1.5" style="-webkit-tap-highlight-color: rgba(0, 0, 0, 0);">
            <use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#raphael-marker-block" transform="rotate(180 1.5 1.5) scale(0.6,0.6)" stroke-width="1.6667" fill="black" stroke="none" style="-webkit-tap-highlight-color: rgba(0, 0, 0, 0);"></use>
        </marker>
        <marker id="raphael-marker-endblock33-obj12sie" markerHeight="3" markerWidth="3" orient="auto" refX="1.5" refY="1.5" style="-webkit-tap-highlight-color: rgba(0, 0, 0, 0);">
            <use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#raphael-marker-block" transform="rotate(180 1.5 1.5) scale(0.6,0.6)" stroke-width="1.6667" fill="black" stroke="none" style="-webkit-tap-highlight-color: rgba(0, 0, 0, 0);"></use>
        </marker>
        <marker id="raphael-marker-endblock33-objsiug7" markerHeight="3" markerWidth="3" orient="auto" refX="1.5" refY="1.5" style="-webkit-tap-highlight-color: rgba(0, 0, 0, 0);">
            <use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#raphael-marker-block" transform="rotate(180 1.5 1.5) scale(0.6,0.6)" stroke-width="1.6667" fill="black" stroke="none" style="-webkit-tap-highlight-color: rgba(0, 0, 0, 0);"></use>
        </marker>
        <marker id="raphael-marker-endblock33-objm6qqx" markerHeight="3" markerWidth="3" orient="auto" refX="1.5" refY="1.5" style="-webkit-tap-highlight-color: rgba(0, 0, 0, 0);">
            <use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#raphael-marker-block" transform="rotate(180 1.5 1.5) scale(0.6,0.6)" stroke-width="1.6667" fill="black" stroke="none" style="-webkit-tap-highlight-color: rgba(0, 0, 0, 0);"></use>
        </marker>
        <marker id="raphael-marker-endblock33-obj5eszy" markerHeight="3" markerWidth="3" orient="auto" refX="1.5" refY="1.5" style="-webkit-tap-highlight-color: rgba(0, 0, 0, 0);">
            <use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#raphael-marker-block" transform="rotate(180 1.5 1.5) scale(0.6,0.6)" stroke-width="1.6667" fill="black" stroke="none" style="-webkit-tap-highlight-color: rgba(0, 0, 0, 0);"></use>
        </marker>
        <marker id="raphael-marker-endblock33-objy6hp2" markerHeight="3" markerWidth="3" orient="auto" refX="1.5" refY="1.5" style="-webkit-tap-highlight-color: rgba(0, 0, 0, 0);">
            <use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#raphael-marker-block" transform="rotate(180 1.5 1.5) scale(0.6,0.6)" stroke-width="1.6667" fill="black" stroke="none" style="-webkit-tap-highlight-color: rgba(0, 0, 0, 0);"></use>
        </marker>
        <marker id="raphael-marker-endblock33-objbv2wl" markerHeight="3" markerWidth="3" orient="auto" refX="1.5" refY="1.5" style="-webkit-tap-highlight-color: rgba(0, 0, 0, 0);">
            <use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#raphael-marker-block" transform="rotate(180 1.5 1.5) scale(0.6,0.6)" stroke-width="1.6667" fill="black" stroke="none" style="-webkit-tap-highlight-color: rgba(0, 0, 0, 0);"></use>
        </marker>
    </defs>
    <rect x="0" y="0" width="129.09375" height="38" rx="20" ry="20" fill="none" stroke="#000000" style="-webkit-tap-highlight-color: rgba(0, 0, 0, 0);" stroke-width="2" class="flowchart" id="app" transform="matrix(1,0,0,1,43.7734,37.1602)"></rect>
    <text x="10" y="19" text-anchor="start" font-family="'Andale Mono', monospace" font-size="16px" stroke="none" fill="#000000" style="-webkit-tap-highlight-color: rgba(0, 0, 0, 0); text-anchor: start; font-family: &quot;Andale Mono&quot;, monospace; font-size: 16px;" id="appt" class="flowchartt" transform="matrix(1,0,0,1,43.7734,37.1602)" stroke-width="1">
        <tspan style="-webkit-tap-highlight-color: rgba(0, 0, 0, 0);" dy="5.5">application</tspan>
    </text>
    <path fill="none" stroke="#000000" d="M37.236328125,18.6181640625L0,37.236328125L74.47265625,74.47265625L148.9453125,37.236328125L74.47265625,0L0,37.236328125" stroke-width="2" font-family="'Andale Mono', monospace" id="start" class="flowchart" style="-webkit-tap-highlight-color: rgba(0, 0, 0, 0); font-family: &quot;Andale Mono&quot;, monospace;" transform="matrix(1,0,0,1,33.8477,144.084)"></path>
    <text x="42.236328125" y="37.236328125" text-anchor="start" font-family="'Andale Mono', monospace" font-size="16px" stroke="none" fill="#000000" style="-webkit-tap-highlight-color: rgba(0, 0, 0, 0); text-anchor: start; font-family: &quot;Andale Mono&quot;, monospace; font-size: 16px;" id="startt" class="flowchartt" transform="matrix(1,0,0,1,33.8477,144.084)" stroke-width="1">
        <tspan style="-webkit-tap-highlight-color: rgba(0, 0, 0, 0);" dy="5.501953125">Pwnable</tspan>
    </text>
    <path fill="none" stroke="#000000" d="M37.236328125,18.6181640625L0,37.236328125L74.47265625,74.47265625L148.9453125,37.236328125L74.47265625,0L0,37.236328125" stroke-width="2" font-family="'Andale Mono', monospace" id="pwn" class="flowchart" style="-webkit-tap-highlight-color: rgba(0, 0, 0, 0); font-family: &quot;Andale Mono&quot;, monospace;" transform="matrix(1,0,0,1,266.6406,144.084)"></path>
    <text x="42.236328125" y="37.236328125" text-anchor="start" font-family="'Andale Mono', monospace" font-size="16px" stroke="none" fill="#000000" style="-webkit-tap-highlight-color: rgba(0, 0, 0, 0); text-anchor: start; font-family: &quot;Andale Mono&quot;, monospace; font-size: 16px;" id="pwnt" class="flowchartt" transform="matrix(1,0,0,1,266.6406,144.084)" stroke-width="1">
        <tspan style="-webkit-tap-highlight-color: rgba(0, 0, 0, 0);" dy="5.501953125">Windows</tspan>
    </text>
    <rect x="0" y="0" width="99.25" height="38" rx="0" ry="0" fill="none" stroke="#000000" style="-webkit-tap-highlight-color: rgba(0, 0, 0, 0);" stroke-width="2" class="flowchart" id="bug" transform="matrix(1,0,0,1,524.2813,162.3203)"></rect>
    <text x="10" y="19" text-anchor="start" font-family="'Andale Mono', monospace" font-size="16px" stroke="none" fill="#000000" style="-webkit-tap-highlight-color: rgba(0, 0, 0, 0); text-anchor: start; font-family: &quot;Andale Mono&quot;, monospace; font-size: 16px;" id="bugt" class="flowchartt" transform="matrix(1,0,0,1,524.2813,162.3203)" stroke-width="1">
        <tspan style="-webkit-tap-highlight-color: rgba(0, 0, 0, 0);" dy="5.5">analysis</tspan>
    </text>
    <path fill="none" stroke="#000000" d="M44.701171875,22.3505859375L0,44.701171875L89.40234375,89.40234375L178.8046875,44.701171875L89.40234375,0L0,44.701171875" stroke-width="2" font-family="'Andale Mono', monospace" id="find" class="flowchart" style="-webkit-tap-highlight-color: rgba(0, 0, 0, 0); font-family: &quot;Andale Mono&quot;, monospace;" transform="matrix(1,0,0,1,484.5039,261.7793)"></path>
    <text x="49.701171875" y="44.701171875" text-anchor="start" font-family="'Andale Mono', monospace" font-size="16px" stroke="none" fill="#000000" style="-webkit-tap-highlight-color: rgba(0, 0, 0, 0); text-anchor: start; font-family: &quot;Andale Mono&quot;, monospace; font-size: 16px;" id="findt" class="flowchartt" transform="matrix(1,0,0,1,484.5039,261.7793)" stroke-width="1">
        <tspan style="-webkit-tap-highlight-color: rgba(0, 0, 0, 0);" dy="5.513671875">bug found</tspan>
    </text>
    <rect x="0" y="0" width="89.296875" height="38" rx="0" ry="0" fill="none" stroke="#000000" style="-webkit-tap-highlight-color: rgba(0, 0, 0, 0);" stroke-width="2" class="flowchart" id="exp" transform="matrix(1,0,0,1,776.9805,287.4805)"></rect>
    <text x="10" y="19" text-anchor="start" font-family="'Andale Mono', monospace" font-size="16px" stroke="none" fill="#000000" style="-webkit-tap-highlight-color: rgba(0, 0, 0, 0); text-anchor: start; font-family: &quot;Andale Mono&quot;, monospace; font-size: 16px;" id="expt" class="flowchartt" transform="matrix(1,0,0,1,776.9805,287.4805)" stroke-width="1">
        <tspan style="-webkit-tap-highlight-color: rgba(0, 0, 0, 0);" dy="5.5">exploit</tspan>
    </text>
    <path fill="none" stroke="#000000" d="M40.96875,20.484375L0,40.96875L81.9375,81.9375L163.875,40.96875L81.9375,0L0,40.96875" stroke-width="2" font-family="'Andale Mono', monospace" id="exps" class="flowchart" style="-webkit-tap-highlight-color: rgba(0, 0, 0, 0); font-family: &quot;Andale Mono&quot;, monospace;" transform="matrix(1,0,0,1,739.6914,390.6719)"></path>
    <text x="45.96875" y="40.96875" text-anchor="start" font-family="'Andale Mono', monospace" font-size="16px" stroke="none" fill="#000000" style="-webkit-tap-highlight-color: rgba(0, 0, 0, 0); text-anchor: start; font-family: &quot;Andale Mono&quot;, monospace; font-size: 16px;" id="expst" class="flowchartt" transform="matrix(1,0,0,1,739.6914,390.6719)" stroke-width="1">
        <tspan style="-webkit-tap-highlight-color: rgba(0, 0, 0, 0);" dy="5.5">can work</tspan>
    </text>
    <rect x="0" y="0" width="158.953125" height="38" rx="20" ry="20" fill="none" stroke="#000000" style="-webkit-tap-highlight-color: rgba(0, 0, 0, 0);" stroke-width="2" class="flowchart" id="end" transform="matrix(1,0,0,1,742.1523,559.7695)"></rect>
    <text x="10" y="19" text-anchor="start" font-family="'Andale Mono', monospace" font-size="16px" stroke="none" fill="#000000" style="-webkit-tap-highlight-color: rgba(0, 0, 0, 0); text-anchor: start; font-family: &quot;Andale Mono&quot;, monospace; font-size: 16px;" id="endt" class="flowchartt" transform="matrix(1,0,0,1,742.1523,559.7695)" stroke-width="1">
        <tspan style="-webkit-tap-highlight-color: rgba(0, 0, 0, 0);" dy="5.5">Congratulation</tspan>
    </text>
    <path fill="none" stroke="#000000" d="M52.16015625,26.080078125L0,52.16015625L104.3203125,104.3203125L208.640625,52.16015625L104.3203125,0L0,52.16015625" stroke-width="2" font-family="'Andale Mono', monospace" id="otherbug" class="flowchart" style="-webkit-tap-highlight-color: rgba(0, 0, 0, 0); font-family: &quot;Andale Mono&quot;, monospace;" transform="matrix(1,0,0,1,957.5664,379.4805)"></path>
    <text x="57.16015625" y="52.16015625" text-anchor="start" font-family="'Andale Mono', monospace" font-size="16px" stroke="none" fill="#000000" style="-webkit-tap-highlight-color: rgba(0, 0, 0, 0); text-anchor: start; font-family: &quot;Andale Mono&quot;, monospace; font-size: 16px;" id="otherbugt" class="flowchartt" transform="matrix(1,0,0,1,957.5664,379.4805)" stroke-width="1">
        <tspan style="-webkit-tap-highlight-color: rgba(0, 0, 0, 0);" dy="5.50390625">exploitable</tspan>
        <tspan dy="19.2" x="57.16015625" style="-webkit-tap-highlight-color: rgba(0, 0, 0, 0);"></tspan>
    </text>
    <rect x="0" y="0" width="79.34375" height="38" rx="20" ry="20" fill="none" stroke="#000000" style="-webkit-tap-highlight-color: rgba(0, 0, 0, 0);" stroke-width="2" class="flowchart" id="gan" transform="matrix(1,0,0,1,301.4414,305.7168)"></rect>
    <text x="10" y="19" text-anchor="start" font-family="'Andale Mono', monospace" font-size="16px" stroke="none" fill="#000000" style="-webkit-tap-highlight-color: rgba(0, 0, 0, 0); text-anchor: start; font-family: &quot;Andale Mono&quot;, monospace; font-size: 16px;" id="gant" class="flowchartt" transform="matrix(1,0,0,1,301.4414,305.7168)" stroke-width="1">
        <tspan style="-webkit-tap-highlight-color: rgba(0, 0, 0, 0);" dy="5.5">gan...</tspan>
    </text>
    <rect x="0" y="0" width="79.34375" height="38" rx="20" ry="20" fill="none" stroke="#000000" style="-webkit-tap-highlight-color: rgba(0, 0, 0, 0);" stroke-width="2" class="flowchart" id="dispwn" transform="matrix(1,0,0,1,68.6484,305.7168)"></rect>
    <text x="10" y="19" text-anchor="start" font-family="'Andale Mono', monospace" font-size="16px" stroke="none" fill="#000000" style="-webkit-tap-highlight-color: rgba(0, 0, 0, 0); text-anchor: start; font-family: &quot;Andale Mono&quot;, monospace; font-size: 16px;" id="dispwnt" class="flowchartt" transform="matrix(1,0,0,1,68.6484,305.7168)" stroke-width="1">
        <tspan style="-webkit-tap-highlight-color: rgba(0, 0, 0, 0);" dy="5.5">byebye</tspan>
    </text>
    <path fill="none" stroke="#000000" d="M108.3203125,75.16015625C108.3203125,75.16015625,108.3203125,127.81223814375699,108.3203125,141.07809471464498" stroke-width="2" marker-end="url(#raphael-marker-endblock33-obj7zr63)" font-family="'Andale Mono', monospace" style="-webkit-tap-highlight-color: rgba(0, 0, 0, 0); font-family: &quot;Andale Mono&quot;, monospace;"></path>
    <path fill="none" stroke="#000000" d="M182.79296875,181.3203125C182.79296875,181.3203125,248.6472905660048,181.3203125,263.63172121359185,181.3203125" stroke-width="2" marker-end="url(#raphael-marker-endblock33-objcsbyd)" font-family="'Andale Mono', monospace" style="-webkit-tap-highlight-color: rgba(0, 0, 0, 0); font-family: &quot;Andale Mono&quot;, monospace;"></path>
    <text x="187.79296875" y="171.3203125" text-anchor="start" font-family="'Andale Mono', monospace" font-size="16px" stroke="none" fill="#000000" style="-webkit-tap-highlight-color: rgba(0, 0, 0, 0); text-anchor: start; font-family: &quot;Andale Mono&quot;, monospace; font-size: 16px;" stroke-width="1">
        <tspan style="-webkit-tap-highlight-color: rgba(0, 0, 0, 0);" dy="5.5078125">yes</tspan>
    </text>
    <path fill="none" stroke="#000000" d="M108.3203125,218.556640625C108.3203125,218.556640625,108.3203125,287.39030207693577,108.3203125,302.71654700959334" stroke-width="2" marker-end="url(#raphael-marker-endblock33-objyv21f)" font-family="'Andale Mono', monospace" style="-webkit-tap-highlight-color: rgba(0, 0, 0, 0); font-family: &quot;Andale Mono&quot;, monospace;"></path>
    <text x="113.3203125" y="228.556640625" text-anchor="start" font-family="'Andale Mono', monospace" font-size="16px" stroke="none" fill="#000000" style="-webkit-tap-highlight-color: rgba(0, 0, 0, 0); text-anchor: start; font-family: &quot;Andale Mono&quot;, monospace; font-size: 16px;" stroke-width="1">
        <tspan style="-webkit-tap-highlight-color: rgba(0, 0, 0, 0);" dy="5.509765625">no</tspan>
    </text>
    <path fill="none" stroke="#000000" d="M415.5859375,181.3203125C415.5859375,181.3203125,503.80118397064507,181.3203125,521.2891674018374,181.3203125" stroke-width="2" marker-end="url(#raphael-marker-endblock33-objff9q1)" font-family="'Andale Mono', monospace" style="-webkit-tap-highlight-color: rgba(0, 0, 0, 0); font-family: &quot;Andale Mono&quot;, monospace;"></path>
    <text x="420.5859375" y="171.3203125" text-anchor="start" font-family="'Andale Mono', monospace" font-size="16px" stroke="none" fill="#000000" style="-webkit-tap-highlight-color: rgba(0, 0, 0, 0); text-anchor: start; font-family: &quot;Andale Mono&quot;, monospace; font-size: 16px;" stroke-width="1">
        <tspan style="-webkit-tap-highlight-color: rgba(0, 0, 0, 0);" dy="5.5078125">yes</tspan>
    </text>
    <path fill="none" stroke="#000000" d="M341.11328125,218.556640625C341.11328125,218.556640625,341.11328125,287.39030207693577,341.11328125,302.71654700959334" stroke-width="2" marker-end="url(#raphael-marker-endblock33-objbp56f)" font-family="'Andale Mono', monospace" style="-webkit-tap-highlight-color: rgba(0, 0, 0, 0); font-family: &quot;Andale Mono&quot;, monospace;"></path>
    <text x="346.11328125" y="228.556640625" text-anchor="start" font-family="'Andale Mono', monospace" font-size="16px" stroke="none" fill="#000000" style="-webkit-tap-highlight-color: rgba(0, 0, 0, 0); text-anchor: start; font-family: &quot;Andale Mono&quot;, monospace; font-size: 16px;" stroke-width="1">
        <tspan style="-webkit-tap-highlight-color: rgba(0, 0, 0, 0);" dy="5.509765625">no</tspan>
    </text>
    <path fill="none" stroke="#000000" d="M573.90625,200.3203125C573.90625,200.3203125,573.90625,246.43430297635496,573.90625,258.7733980842859" stroke-width="2" marker-end="url(#raphael-marker-endblock33-objfgo63)" font-family="'Andale Mono', monospace" style="-webkit-tap-highlight-color: rgba(0, 0, 0, 0); font-family: &quot;Andale Mono&quot;, monospace;"></path>
    <path fill="none" stroke="#000000" d="M663.30859375,306.48046875C663.30859375,306.48046875,756.0133017627522,306.48046875,773.9838921343649,306.48046875" stroke-width="2" marker-end="url(#raphael-marker-endblock33-obj540te)" font-family="'Andale Mono', monospace" style="-webkit-tap-highlight-color: rgba(0, 0, 0, 0); font-family: &quot;Andale Mono&quot;, monospace;"></path>
    <text x="668.30859375" y="296.48046875" text-anchor="start" font-family="'Andale Mono', monospace" font-size="16px" stroke="none" fill="#000000" style="-webkit-tap-highlight-color: rgba(0, 0, 0, 0); text-anchor: start; font-family: &quot;Andale Mono&quot;, monospace; font-size: 16px;" stroke-width="1">
        <tspan style="-webkit-tap-highlight-color: rgba(0, 0, 0, 0);" dy="5.51171875">yes</tspan>
    </text>
    <path fill="none" stroke="#000000" d="M573.90625,351.181640625C573.90625,351.181640625,573.90625,376.181640625,573.90625,376.181640625C573.90625,376.181640625,688.30859375,376.181640625,688.30859375,376.181640625C688.30859375,376.181640625,688.30859375,310.48046875,688.30859375,310.48046875C688.30859375,310.48046875,696.30859375,306.48046875,688.30859375,302.48046875C688.30859375,302.48046875,688.30859375,137.3203125,688.30859375,137.3203125C688.30859375,137.3203125,573.90625,137.3203125,573.90625,137.3203125C573.90625,137.3203125,573.90625,152.69375705718994,573.90625,159.32956027425826" stroke-width="2" marker-end="url(#raphael-marker-endblock33-obj12sie)" font-family="'Andale Mono', monospace" style="-webkit-tap-highlight-color: rgba(0, 0, 0, 0); font-family: &quot;Andale Mono&quot;, monospace;"></path>
    <text x="578.90625" y="361.181640625" text-anchor="start" font-family="'Andale Mono', monospace" font-size="16px" stroke="none" fill="#000000" style="-webkit-tap-highlight-color: rgba(0, 0, 0, 0); text-anchor: start; font-family: &quot;Andale Mono&quot;, monospace; font-size: 16px;" stroke-width="1">
        <tspan style="-webkit-tap-highlight-color: rgba(0, 0, 0, 0);" dy="5.509765625">no</tspan>
    </text>
    <path fill="none" stroke="#000000" d="M821.62890625,325.48046875C821.62890625,325.48046875,821.62890625,374.89254820439965,821.62890625,387.67985392257924" stroke-width="2" marker-end="url(#raphael-marker-endblock33-objsiug7)" font-family="'Andale Mono', monospace" style="-webkit-tap-highlight-color: rgba(0, 0, 0, 0); font-family: &quot;Andale Mono&quot;, monospace;"></path>
    <path fill="none" stroke="#000000" d="M821.62890625,472.609375C821.62890625,472.609375,821.62890625,541.4430364519358,821.62890625,556.7692813845933" stroke-width="2" marker-end="url(#raphael-marker-endblock33-objm6qqx)" font-family="'Andale Mono', monospace" style="-webkit-tap-highlight-color: rgba(0, 0, 0, 0); font-family: &quot;Andale Mono&quot;, monospace;"></path>
    <text x="826.62890625" y="482.609375" text-anchor="start" font-family="'Andale Mono', monospace" font-size="16px" stroke="none" fill="#000000" style="-webkit-tap-highlight-color: rgba(0, 0, 0, 0); text-anchor: start; font-family: &quot;Andale Mono&quot;, monospace; font-size: 16px;" stroke-width="1">
        <tspan style="-webkit-tap-highlight-color: rgba(0, 0, 0, 0);" dy="5.5">yes</tspan>
    </text>
    <path fill="none" stroke="#000000" d="M903.56640625,431.640625C903.56640625,431.640625,943.2205061912537,431.640625,954.5668453346007,431.640625" stroke-width="2" marker-end="url(#raphael-marker-endblock33-obj5eszy)" font-family="'Andale Mono', monospace" style="-webkit-tap-highlight-color: rgba(0, 0, 0, 0); font-family: &quot;Andale Mono&quot;, monospace;"></path>
    <text x="908.56640625" y="421.640625" text-anchor="start" font-family="'Andale Mono', monospace" font-size="16px" stroke="none" fill="#000000" style="-webkit-tap-highlight-color: rgba(0, 0, 0, 0); text-anchor: start; font-family: &quot;Andale Mono&quot;, monospace; font-size: 16px;" stroke-width="1">
        <tspan style="-webkit-tap-highlight-color: rgba(0, 0, 0, 0);" dy="5.5">no</tspan>
    </text>
    <path fill="none" stroke="#000000" d="M1061.88671875,483.80078125C1061.88671875,483.80078125,1061.88671875,508.80078125,1061.88671875,508.80078125C1061.88671875,508.80078125,1182.015625,508.80078125,1182.015625,508.80078125C1182.015625,508.80078125,1182.015625,262.48046875,1182.015625,262.48046875C1182.015625,262.48046875,821.62890625,262.48046875,821.62890625,262.48046875C821.62890625,262.48046875,821.62890625,277.85391330718994,821.62890625,284.48971652425826" stroke-width="2" marker-end="url(#raphael-marker-endblock33-objy6hp2)" font-family="'Andale Mono', monospace" style="-webkit-tap-highlight-color: rgba(0, 0, 0, 0); font-family: &quot;Andale Mono&quot;, monospace;"></path>
    <text x="1066.88671875" y="493.80078125" text-anchor="start" font-family="'Andale Mono', monospace" font-size="16px" stroke="none" fill="#000000" style="-webkit-tap-highlight-color: rgba(0, 0, 0, 0); text-anchor: start; font-family: &quot;Andale Mono&quot;, monospace; font-size: 16px;" stroke-width="1">
        <tspan style="-webkit-tap-highlight-color: rgba(0, 0, 0, 0);" dy="5.50390625">yes</tspan>
    </text>
    <path fill="none" stroke="#000000" d="M1166.20703125,431.640625C1166.20703125,431.640625,1178.015625,431.640625,1178.015625,431.640625C1178.015625,431.640625,1182.015625,423.640625,1186.015625,431.640625C1186.015625,431.640625,1191.20703125,431.640625,1191.20703125,431.640625C1191.20703125,431.640625,1191.20703125,137.3203125,1191.20703125,137.3203125C1191.20703125,137.3203125,573.90625,137.3203125,573.90625,137.3203125C573.90625,137.3203125,573.90625,152.69375705718994,573.90625,159.32956027425826" stroke-width="2" marker-end="url(#raphael-marker-endblock33-objbv2wl)" font-family="'Andale Mono', monospace" style="-webkit-tap-highlight-color: rgba(0, 0, 0, 0); font-family: &quot;Andale Mono&quot;, monospace;"></path>
    <text x="1171.20703125" y="421.640625" text-anchor="start" font-family="'Andale Mono', monospace" font-size="16px" stroke="none" fill="#000000" style="-webkit-tap-highlight-color: rgba(0, 0, 0, 0); text-anchor: start; font-family: &quot;Andale Mono&quot;, monospace; font-size: 16px;" stroke-width="1">
        <tspan style="-webkit-tap-highlight-color: rgba(0, 0, 0, 0);" dy="5.5">no</tspan>
    </text>
</svg>

--


# Tool

* ncat
* qira
* pwntool

---

# Service

```shell
ncat -vc./bin -kl 8888
```

```shell
qira -s ./bin
```

--

# Connect

```shell
cat payload - | nc pwn.ctf.com 5566
```

---

# Pwntool

--

# Basic

|     Function      |            Effect             |           Example           |
|        ---        |              ---              |             ---             |
|  remote(ip,port)  |      connect to service       | io=remote('127.0.0.1',5566) |
|   process(bin)    | execute local file as service |     io=process('./bin')     |
| recvuntil(patten) |   receive until got patten    |      io.recvline(": ")      |
|    recvline()     |        recvuntil("\n")        |        io.recvline()        |
|    send(data)     |           send data           |       io.send("8787")       |
|  sendline(data)   |        send(data+"\n")        |     io.sendline("8787")     |
|   interative()    |         stdin+stdout          |      io.interactive()       |
|      close()      |       close connection        |         io.close()          |

--

# Advance

|     Function      |          Effect           |       Example        |
|        ---        |            ---            |         ---          |
|     u32(text)     |        text -> int        |     u32("8787")      |
|    p32(number)    |        int -> text        |   p32(0x37383738)    |
|    flat(list)     |  int -> text (recursive)  |    flat(ropchin)     |
|  cyclic(number)   |  generate special patten  |     cyclic(100)      |
| cyclic_find(text) | padding of special patten | cyclic_find("aabc")  |
|      context      |        setting env        | context.arch="arm64" |
|     ELF(bin)      |   local elf infomation    |     ELF('./bin')     |
|        gdb        |  attach process to debug  |    gdb.attach(io)    |
|     asm(text)     |      asm to obj code      |   asm('pop eax;')    |
|    shellcraft     |    shellcode database     |   shellcraft.sh()    |

--

# Other

b64e, b64d, randoms, urlencode, xor, md5sum, sha1sum, mbruteforce

---

# Demo

1. qira + remote
1. process + gdb

```c
#include <stdio.h>
int main(int argc, char *argv[])
{
    char c[100];
    gets(c);
    puts(c);
    return 0;
}
```

--

#Practice

## Hello
nc vpn.duckll.tw 8787

```python
#!/usr/bin/env python
# -*- coding: utf-8 -*-

import signal,sys, os
from pwn import *

def alarm(time):
    def handler(signum, frame):
        print 'Timeout'
        exit()
    signal.signal(signal.SIGALRM, handler)
    signal.alarm(time)

sys.stdout = os.fdopen(sys.stdout.fileno(), 'w', 0)
sys.stdin = os.fdopen(sys.stdin.fileno(), 'r', 0)
alarm(5)

name=raw_input("Your name: ")
print "Hello", name
ho=sha512sumhex(name)
print "This is your hash: ", ho
hh=raw_input("Show your hash reversed string: ")
if hh==ho[::-1] :
    print "{{flag}}"
else :
    print "Try again"
```

--

## MD5
nc vpn.duckll.tw 8788

```python
#!/usr/bin/env python
# -*- coding: utf-8 -*-

import sys, os
from pwn import *

def alarm(time):
    def handler(signum, frame):
        print 'Timeout'
        exit()
    signal.signal(signal.SIGALRM, handler)
    signal.alarm(time)

sys.stdout = os.fdopen(sys.stdout.fileno(), 'w', 0)
sys.stdin = os.fdopen(sys.stdin.fileno(), 'r', 0)
alarm(10)

rnd=randoms(20)
print "Try to break challenge", rnd
io=raw_input()
if md5sumhex(rnd+io)[:5]=='fffff':
    print "{{flag}}"
else :
    print "Try again"
```

---

#Q & A

--

#END

