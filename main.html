<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Box Factory Escape - 3D Prototype</title>
  <style>
    body {
      margin: 0;
      overflow: hidden;
      font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
      background: #111;
      color: #fff;
      user-select: none;
    }
    #ui {
      position: absolute;
      top: 16px;
      left: 16px;
      background: rgba(0, 0, 0, 0.75);
      padding: 14px 18px;
      border-radius: 8px;
      border: 1px solid #444;
      pointer-events: none;
      z-index: 10;
      width: 280px;
    }
    h1 {
      font-size: 16px;
      margin: 0 0 8px 0;
      text-transform: uppercase;
      letter-spacing: 1px;
      color: #f39c12;
    }
    .stat {
      font-size: 13px;
      margin-bottom: 6px;
    }
    .bar-bg {
      width: 100%;
      height: 12px;
      background: #333;
      border-radius: 6px;
      overflow: hidden;
      margin-top: 4px;
    }
    #quota-bar {
      width: 100%;
      height: 100%;
      background: #2ecc71;
      transition: width 0.1s linear, background 0.2s;
    }
    #overlay {
      position: absolute;
      inset: 0;
      background: rgba(0, 0, 0, 0.82);
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      z-index: 20;
      text-align: center;
      padding: 20px;
    }
    #overlay h2 {
      font-size: 32px;
      margin-bottom: 10px;
    }
    #overlay p {
      max-width: 460px;
      color: #ccc;
      line-height: 1.5;
      margin-bottom: 20px;
    }
    button {
      padding: 12px 26px;
      font-size: 16px;
      font-weight: bold;
      background: #e67e22;
      color: white;
      border: none;
      border-radius: 6px;
      cursor: pointer;
    }
    button:hover {
      background: #d35400;
    }
    #prompt {
      position: absolute;
      bottom: 25%;
      left: 50%;
      transform: translateX(-50%);
      background: rgba(0, 0, 0, 0.8);
      padding: 8px 16px;
      border-radius: 4px;
      font-size: 14px;
      display: none;
      pointer-events: none;
    }
  </style>
</head>
<body>

<div id="ui">
  <h1>Shift Status</h1>
  <div class="stat">Objective: <b>Reach the Green Exit Door</b></div>
  <div class="stat">Boxes Packed: <span id="box-count">0</span></div>
  <div class="stat">
    Work Compliance Quota:
    <div class="bar-bg"><div id="quota-bar"></div></div>
  </div>
  <div class="stat" style="color:#aaa; font-size:11px; margin-top:8px;">
    Controls: <b>WASD</b> Move | <b>Mouse</b> Look | Hold <b>E</b> at Work Table to Pack Boxes
  </div>
</div>

<div id="prompt">Hold [E] to Pack Box & Refill Quota</div>

<div id="overlay">
  <h2 id="overlay-title">SECTOR 7 BOX FACTORY</h2>
  <p id="overlay-desc">
    Maintain your Work Compliance Quota at the blue workbench so the Floor Managers don't sound the alarm. When their backs are turned, sneak behind the cardboard pallets and reach the glowing green Exit Door at the far end of the warehouse.
  </p>
  <button id="start-btn">Start Shift</button>
</div>

<script src="https://cdnjs.cloudflare.com/ajax/libs/three.js/r128/three.min.js"></script>
<script>
  // --- SCENE, CAMERA, RENDERER ---
  const scene = new THREE.Scene();
  scene.background = new THREE.Color(0x1a1c20);
  scene.fog = new THREE.FogExp2(0x1a1c20, 0.018);

  const camera = new THREE.PerspectiveCamera(75, window.innerWidth / window.innerHeight, 0.1, 150);
  const renderer = new THREE.WebGLRenderer({ antialias: true });
  renderer.setSize(window.innerWidth, window.innerHeight);
  renderer.shadowMap.enabled = true;
  document.body.appendChild(renderer.domElement);

  // --- LIGHTING ---
  const ambientLight = new THREE.AmbientLight(0x555566, 0.7);
  scene.add(ambientLight);

  const dirLight = new THREE.DirectionalLight(0xffeedd, 0.8);
  dirLight.position.set(15, 30, 10);
  dirLight.castShadow = true;
  scene.add(dirLight);

  // --- ENVIRONMENT ---
  const floorGeo = new THREE.PlaneGeometry(80, 100);
  const floorMat = new THREE.MeshStandardMaterial({ color: 0x33363b, roughness: 0.9 });
  const floor = new THREE.Mesh(floorGeo, floorMat);
  floor.rotation.x = -Math.PI / 2;
  floor.receiveShadow = true;
  scene.add(floor);

  const obstacles = []; // Bounding boxes for collision & line-of-sight

  function createBoxMesh(w, h, d, x, y, z, color, isCollidable = true) {
    const geo = new THREE.BoxGeometry(w, h, d);
    const mat = new THREE.MeshStandardMaterial({ color, roughness: 0.8 });
    const mesh = new THREE.Mesh(geo, mat);
    mesh.position.set(x, y, z);
    mesh.castShadow = true;
    mesh.receiveShadow = true;
    scene.add(mesh);
    if (isCollidable) {
      obstacles.push(new THREE.Box3().setFromObject(mesh));
    }
    return mesh;
  }

  // Outer Factory Walls
  createBoxMesh(80, 14, 2, 0, 7, -50, 0x222428);
  createBoxMesh(80, 14, 2, 0, 7, 50, 0x222428);
  createBoxMesh(2, 14, 100, -40, 7, 0, 0x222428);
  createBoxMesh(2, 14, 100, 40, 7, 0, 0x222428);

  // Work Station (Start Area at z = 35)
  const workbench = createBoxMesh(6, 1.4, 3, 0, 0.7, 34, 0x2980b9);
  
  // Safe Zone Floor Marker around workbench
  const zoneGeo = new THREE.PlaneGeometry(10, 10);
  const zoneMat = new THREE.MeshBasicMaterial({ color: 0x2980b9, side: THREE.DoubleSide, transparent: true, opacity: 0.25 });
  const workZone = new THREE.Mesh(zoneGeo, zoneMat);
  workZone.rotation.x = -Math.PI / 2;
  workZone.position.set(0, 0.02, 36);
  scene.add(workZone);

  // Exit Door (At z = -48.5)
  const exitDoor = createBoxMesh(5, 5, 1, 0, 2.5, -48.8, 0x2ecc71, false);
  const exitLight = new THREE.PointLight(0x2ecc71, 2, 15);
  exitLight.position.set(0, 4, -46);
  scene.add(exitLight);

  // Cardboard Pallets / Cover Obstacles throughout warehouse
  const palletCoords = [
    [-12, 22], [12, 22], [0, 14],
    [-18, 8], [18, 8], [-7, 2], [8, 2],
    [-15, -10], [0, -10], [15, -10],
    [-10, -24], [10, -24], [0, -34],
    [-22, -32], [22, -32]
  ];
  palletCoords.forEach(([x, z]) => {
    const h = 2.8 + Math.random() * 2;
    createBoxMesh(4.5, h, 4.5, x, h / 2, z, 0xa67c52);
  });

  // --- NPC MANAGERS ---
  const managers = [];
  function createManager(waypoints, speed) {
    const group = new THREE.Group();

    // Body
    const body = new THREE.Mesh(
      new THREE.CylinderGeometry(0.6, 0.6, 2.6, 12),
      new THREE.MeshStandardMaterial({ color: 0xc0392b })
    );
    body.position.y = 1.3;
    group.add(body);

    // Vision Cone Visual
    const coneGeo = new THREE.ConeGeometry(4.5, 14, 16, 1, true);
    coneGeo.rotateX(Math.PI / 2);
    coneGeo.translate(0, 0, 7);
    const coneMat = new THREE.MeshBasicMaterial({
      color: 0xe74c3c,
      transparent: true,
      opacity: 0.22,
      side: THREE.DoubleSide
    });
    const cone = new THREE.Mesh(coneGeo, coneMat);
    cone.position.y = 1.2;
    group.add(cone);

    group.position.set(waypoints[0].x, 0, waypoints[0].z);
    scene.add(group);

    managers.push({
      group,
      waypoints,
      currentWP: 1,
      speed
    });
  }

  createManager([
    { x: -20, z: 18 },
    { x: 20, z: 18 },
    { x: 20, z: -4 },
    { x: -20, z: -4 }
  ], 6.5);

  createManager([
    { x: 22, z: -16 },
    { x: -22, z: -16 },
    { x: -22, z: -38 },
    { x: 22, z: -38 }
  ], 7.5);

  // --- PLAYER & CONTROLS ---
  const player = {
    pos: new THREE.Vector3(0, 1.3, 37),
    yaw: 0,
    pitch: 0,
    speed: 9,
    quota: 100,
    boxesPacked: 0,
    isPlaying: false
  };

  const keys = {};
  window.addEventListener('keydown', e => keys[e.code] = true);
  window.addEventListener('keyup', e => keys[e.code] = false);

  const overlay = document.getElementById('overlay');
  const overlayTitle = document.getElementById('overlay-title');
  const overlayDesc = document.getElementById('overlay-desc');
  const startBtn = document.getElementById('start-btn');
  const quotaBar = document.getElementById('quota-bar');
  const boxCountEl = document.getElementById('box-count');
  const promptEl = document.getElementById('prompt');

  startBtn.addEventListener('click', () => {
    document.body.requestPointerLock();
  });

  document.addEventListener('pointerlockchange', () => {
    if (document.pointerLockElement === document.body) {
      player.isPlaying = true;
      overlay.style.display = 'none';
    } else {
      player.isPlaying = false;
      overlay.style.display = 'flex';
    }
  });

  document.addEventListener('mousemove', e => {
    if (!player.isPlaying) return;
    player.yaw -= e.movementX * 0.0022;
    player.pitch = Math.max(-Math.PI / 3, Math.min(Math.PI / 3, player.pitch - e.movementY * 0.0022));
  });

  function resetGame(title, desc) {
    document.exitPointerLock();
    overlayTitle.textContent = title;
    overlayDesc.textContent = desc;
    startBtn.textContent = 'Try Again';
    player.pos.set(0, 1.3, 37);
    player.yaw = 0;
    player.pitch = 0;
    player.quota = 100;
    player.boxesPacked = 0;
    boxCountEl.textContent = '0';
  }

  // --- GAME LOOP ---
  const raycaster = new THREE.Raycaster();
  let lastTime = performance.now();

  function animate(now) {
    requestAnimationFrame(animate);
    const dt = Math.min((now - lastTime) / 1000, 0.1);
    lastTime = now;

    if (player.isPlaying) {
      // 1. Player Movement
      const forward = new THREE.Vector3(-Math.sin(player.yaw), 0, -Math.cos(player.yaw));
      const right = new THREE.Vector3(Math.cos(player.yaw), 0, -Math.sin(player.yaw));
      const move = new THREE.Vector3();

      if (keys['KeyW'] || keys['ArrowUp']) move.add(forward);
      if (keys['KeyS'] || keys['ArrowDown']) move.sub(forward);
      if (keys['KeyD'] || keys['ArrowRight']) move.add(right);
      if (keys['KeyA'] || keys['ArrowLeft']) move.sub(right);

      if (move.lengthSq() > 0) {
        move.normalize().multiplyScalar(player.speed * dt);
        const nextPos = player.pos.clone().add(move);
        const playerBox = new THREE.Box3().setFromCenterAndSize(nextPos, new THREE.Vector3(1.1, 1.8, 1.1));
        const hit = obstacles.some(b => b.intersectsBox(playerBox));
        if (!hit) player.pos.copy(nextPos);
      }

      camera.position.copy(player.pos);
      camera.rotation.order = 'YXZ';
      camera.rotation.y = player.yaw;
      camera.rotation.x = player.pitch;

      // 2. Workbench & Quota Logic
      const distToBench = player.pos.distanceTo(workbench.position);
      if (distToBench < 4.2) {
        promptEl.style.display = 'block';
        if (keys['KeyE']) {
          player.quota = Math.min(100, player.quota + 35 * dt);
          if (Math.random() < 0.08) {
            player.boxesPacked++;
            boxCountEl.textContent = player.boxesPacked;
          }
        }
      } else {
        promptEl.style.display = 'none';
      }

      player.quota -= 4.2 * dt;
      quotaBar.style.width = Math.max(0, player.quota) + '%';
      quotaBar.style.background = player.quota > 35 ? '#2ecc71' : '#e74c3c';

      if (player.quota <= 0) {
        resetGame('CAUGHT: QUOTA FAILED', 'Your work station went idle for too long and triggered the floor alarm!');
        return;
      }

      // 3. Check Exit Reached
      if (player.pos.distanceTo(exitDoor.position) < 3.5) {
        resetGame('ESCAPED!', `You slipped past the managers and escaped the box factory after packing ${player.boxesPacked} boxes!`);
        return;
      }

      // 4. Update Managers & Line-of-Sight Detection
      const inSafeWorkZone = Math.abs(player.pos.x) < 5 && Math.abs(player.pos.z - 36) < 5;

      for (const m of managers) {
        const target = m.waypoints[m.currentWP];
        const dx = target.x - m.group.position.x;
        const dz = target.z - m.group.position.z;
        const dist = Math.hypot(dx, dz);

        if (dist < 0.4) {
          m.currentWP = (m.currentWP + 1) % m.waypoints.length;
        } else {
          const dirX = dx / dist;
          const dirZ = dz / dist;
          m.group.position.x += dirX * m.speed * dt;
          m.group.position.z += dirZ * m.speed * dt;
          m.group.rotation.y = Math.atan2(dirX, dirZ);
        }

        // Check Vision Cone if player is outside their assigned work zone
        if (!inSafeWorkZone) {
          const toPlayer = new THREE.Vector3().subVectors(player.pos, m.group.position);
          toPlayer.y = 0;
          const distToPlayer = toPlayer.length();

          if (distToPlayer < 14.5) {
            const managerForward = new THREE.Vector3(
              Math.sin(m.group.rotation.y),
              0,
              Math.cos(m.group.rotation.y)
            );
            const angle = managerForward.angleTo(toPlayer.clone().normalize());
            if (angle < 0.48) {
              // Raycast to check if hidden behind cardboard boxes
              const eyePos = m.group.position.clone().add(new THREE.Vector3(0, 1.3, 0));
              const rayDir = new THREE.Vector3().subVectors(player.pos, eyePos).normalize();
              raycaster.set(eyePos, rayDir);

              let blocked = false;
              for (const box of obstacles) {
                const hitPoint = raycaster.ray.intersectBox(box, new THREE.Vector3());
                if (hitPoint && eyePos.distanceTo(hitPoint) < distToPlayer) {
                  blocked = true;
                  break;
                }
              }

              if (!blocked) {
                resetGame('SPOTTED BY MANAGER!', 'A floor manager caught you sneaking away from your assigned workstation.');
                return;
              }
            }
          }
        }
      }
    }

    renderer.render(scene, camera);
  }

  window.addEventListener('resize', () => {
    camera.aspect = window.innerWidth / window.innerHeight;
    camera.updateProjectionMatrix();
    renderer.setSize(window.innerWidth, window.innerHeight);
  });

  requestAnimationFrame(animate);
</script>
</body>
</html>
