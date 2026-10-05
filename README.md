<div align="center">

<img src="img/header.svg" width="100%" alt="Belenus, a semi-rage Counter-Strike 2 internal with a real-time 3D interface">

<br><br>

<img src="img/stack.svg" width="640" alt="C++20, DirectX 11, Dear ImGui, Source 2, Python tooling, in development">

<br><br>

<kbd><img src="img/1.png" width="100%" alt="Weapon and hand chams in first person"></kbd>

<br><br>

<img src="img/stats.svg" width="100%" alt="400+ settings, 27 custom models, 160 bone GPU skinning, 4K ready interface">

</div>

<h2>About</h2>

<p>
<b>Belenus</b> is a semi-rage Counter-Strike 2 internal written from scratch in C++20. It is one DLL that hooks the renderer and the scene system, draws its own interface over the game, and changes what the engine renders instead of painting on top of it. The name is the Celtic god of light.
</p>

<p>
The menu is not a list of checkboxes. The agent stands in a real map with baked lighting, the first-person arms hold the rifle with the game's own animations, and a material you pick is drawn the way the engine will draw it.
</p>

<table>
<tr>
<td width="33%" valign="top">
<b>Drawn by the engine</b><br><br>
Chams are real Source 2 materials, built at run time and swapped into the scene per mesh. Nothing is painted over the finished frame.
</td>
<td width="33%" valign="top">
<b>Seen before the match</b><br><br>
The menu carries its own renderer. Players, weapon and hands are previewed with the same numbers the game material is built from.
</td>
<td width="33%" valign="top">
<b>One source of truth</b><br><br>
Every setting lives in one generated table. Profiles, binds, search and migration between versions all read it.
</td>
</tr>
</table>

<h2>In the game</h2>

<img align="right" width="52%" src="img/3.png" alt="Player chams and ESP">

<h3>Player chams and ESP</h3>

<p>Real Source 2 materials, swapped in per mesh and per owner.</p>

<ul>
<li><b>Five looks</b>: ghost, glow, solid, galaxy, metal</li>
<li><b>Through walls</b> in its own colour and opacity</li>
<li><b>ESP</b>: boxes, names, health, skeleton</li>
<li><b>Hit marks</b> on the point that was hit</li>
<li><b>Tracers</b> that leave the muzzle and travel</li>
</ul>

<br clear="both">

<img align="right" width="52%" src="img/2.png" alt="Hand chams">

<h3>Hands and weapon</h3>

<p>Three independent materials: the players, the weapon you hold, and your hands.</p>

<ul>
<li><b>Own</b> look, colour, opacity, brightness, glow</li>
<li><b>Previewed in first person</b> on the real viewmodel</li>
<li><b>Inspect key</b> plays the inspect animation</li>
</ul>

<br clear="both">

<h2>Custom models</h2>

<p>27 player models fitted to the game's skeleton and moved by the game's own animations. Five of them, turning on the menu's renderer:</p>

<img src="img/models.svg" width="100%" alt="Five custom player models turning: Hu Tao, Noa, CJ, a hazmat suit and Claptrap">

<h2>Features</h2>

<img src="img/features.svg" width="100%" alt="Aim: aim assist, hit groups, hit chance, trigger, recoil control, silent aim. Chams: players, weapon and hands, five looks, through walls. Visuals: player ESP, removals, grenade markers, hit marks, tracers, kill effects. World: weather, fog, sky, exposure, world materials, third person, field of view. Models: weapon models, finishes, 27 custom player models. Movement: bunny hop, auto strafe, air acceleration, slow walk.">

<h2>Engineering</h2>

<img src="img/pipeline.svg" width="100%" alt="In the game: scene system, classifier, material factory, engine frame. In the menu: game packages, asset pipeline, preview renderer, Afterglow UI. The material factory and the preview renderer use the same numbers.">

<br><br>

<table>
<tr>
<td width="50%" valign="top">
<b>A renderer inside the menu</b><br><br>
A dedicated D3D11 pipeline with 4x MSAA: maps exported from the game with their baked lightmaps (400k+ triangles), GPU skinning up to 160 bones, two 2048² shadow maps with PCF, depth of field, and a bloom pass for emissive materials.
</td>
<td width="50%" valign="top">
<b>Engine-level materials</b><br><br>
Materials are written as KV3 text, compiled by the engine's own material system and swapped in through the scene system, per mesh and per owner. Emission follows the engine's units, so what a slider says is what the surface emits.
</td>
</tr>
<tr>
<td valign="top">
<b>Afterglow UI kit</b><br><br>
A component library on raw draw lists: its own layout engine, animation system, type scale and DPI handling. A page is a short list of rows, and nothing in it is a stock widget.
</td>
<td valign="top">
<b>Asset pipeline</b><br><br>
Python tooling extracts models, textures, skeletons and animation clips from the game's packages and bakes them into compact binary formats, streamed in on a worker thread.
</td>
</tr>
<tr>
<td valign="top">
<b>UI harness</b><br><br>
The interface compiles and runs on its own, outside the game. One command renders any page at any resolution to a PNG, which is how the design is iterated and regression-checked.
</td>
<td valign="top">
<b>Generated configuration</b><br><br>
Every setting is collected from the headers into one table at build time. Profiles, binds and migration between versions come from that single source.
</td>
</tr>
</table>

<h2>Latest work</h2>

<ul>
<li><b>Chams</b> rebuilt on engine materials: players, weapon and hands are three materials that share nothing</li>
<li><b>Through walls</b> draws what cover hides flat, in its own colour and opacity</li>
<li><b>Emission</b> is written in the engine's own units, so glow is predictable and capped</li>
<li><b>Menu scene</b> fills the whole window; weapon and hands are shown in first person</li>
<li><b>Hit marks</b> land on the point that was hit, and <b>tracers</b> start at the muzzle</li>
</ul>

<br>

<p align="center"><sub>Source is private. This repository is a showcase.</sub></p>
