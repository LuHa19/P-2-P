<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>P2P Network Simulator</title>
    <style>
        body { 
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif; 
            background-color: #1e1e24; 
            color: #fff; 
            margin: 0; 
            display: flex; 
            flex-direction: column; 
            align-items: center; 
            justify-content: center; 
            height: 100vh; 
        }
        h1 { margin-top: 10px; margin-bottom: 5px; }
        p { color: #aaa; margin-bottom: 20px; text-align: center; max-width: 600px;}
        #controls { margin: 15px 0; }
        button { 
            background-color: #4CAF50; 
            color: white; 
            border: none; 
            padding: 10px 20px; 
            text-align: center; 
            font-size: 16px; 
            cursor: pointer; 
            border-radius: 5px; 
            margin: 0 5px; 
            transition: 0.2s;
        }
        button:hover { background-color: #45a049; }
        button#resetBtn { background-color: #f44336; }
        button#resetBtn:hover { background-color: #da190b; }
        canvas { 
            background-color: #2b2b36; 
            border: 1px solid #444; 
            border-radius: 8px; 
            box-shadow: 0 4px 15px rgba(0,0,0,0.5); 
        }
        .legend { display: flex; gap: 20px; margin-top: 15px; font-size: 14px; }
        .legend-item { display: flex; align-items: center; gap: 8px; }
        .color-box { width: 16px; height: 16px; border-radius: 4px; }
    </style>
</head>
<body>

<h1>Peer-to-Peer (P2P) File Sharing</h1>
<p>Watch how a file is distributed. In a P2P network, clients that download data also act as servers, sharing their downloaded pieces with others.</p>

<div id="controls">
    <button id="addNodeBtn">Add Peer</button>
    <button id="startSharingBtn">Start Sharing</button>
    <button id="resetBtn">Reset Network</button>
</div>

<canvas id="networkCanvas" width="800" height="500"></canvas>

<div class="legend">
    <div class="legend-item"><div class="color-box" style="background: #4CAF50;"></div> Seeder (100% File)</div>
    <div class="legend-item"><div class="color-box" style="background: #FFC107;"></div> Downloading (Partial)</div>
    <div class="legend-item"><div class="color-box" style="background: #F44336;"></div> Leecher (0% File)</div>
</div>

<script>
    const canvas = document.getElementById('networkCanvas');
    const ctx = canvas.getContext('2d');

    let nodes = [];
    let edges = [];
    let packets = [];
    const maxNodes = 15;
    let animationId;
    let isSharing = false;

    class Node {
        constructor(id, x, y) {
            this.id = id;
            this.x = x;
            this.y = y;
            this.status = 'empty'; // empty, partial, full
            this.chunks = 0;
            this.maxChunks = 15; // Total file pieces needed
            this.radius = 22;
        }
        draw() {
            ctx.beginPath();
            ctx.arc(this.x, this.y, this.radius, 0, Math.PI * 2);
            if (this.status === 'full') {
                ctx.fillStyle = '#4CAF50'; 
            } else if (this.status === 'partial') {
                ctx.fillStyle = '#FFC107'; 
            } else {
                ctx.fillStyle = '#F44336'; 
            }
            ctx.fill();
            ctx.strokeStyle = '#fff';
            ctx.lineWidth = 2;
            ctx.stroke();
            
            ctx.fillStyle = '#fff';
            ctx.font = '12px Arial';
            ctx.textAlign = 'center';
            ctx.textBaseline = 'middle';
            ctx.fillText(`P${this.id}`, this.x, this.y);
            
            ctx.font = '11px Arial';
            ctx.fillText(`${Math.round((this.chunks/this.maxChunks)*100)}%`, this.x, this.y + 35);
        }
    }

    class Edge {
        constructor(node1, node2) {
            this.node1 = node1;
            this.node2 = node2;
        }
        draw() {
            ctx.beginPath();
            ctx.moveTo(this.node1.x, this.node1.y);
            ctx.lineTo(this.node2.x, this.node2.y);
            ctx.strokeStyle = 'rgba(255, 255, 255, 0.15)';
            ctx.lineWidth = 2;
            ctx.stroke();
        }
    }

    class Packet {
        constructor(source, target) {
            this.source = source;
            this.target = target;
            this.progress = 0;
            this.speed = 0.01 + Math.random() * 0.015;
        }
        update() {
            this.progress += this.speed;
        }
        draw() {
            const x = this.source.x + (this.target.x - this.source.x) * this.progress;
            const y = this.source.y + (this.target.y - this.source.y) * this.progress;
            ctx.beginPath();
            ctx.arc(x, y, 5, 0, Math.PI * 2);
            ctx.fillStyle = '#00BCD4'; 
            ctx.fill();
            ctx.shadowBlur = 10;
            ctx.shadowColor = '#00BCD4';
            ctx.shadowBlur = 0; // Reset for other drawings
        }
    }

    function initNetwork() {
        nodes = [];
        edges = [];
        packets = [];
        isSharing = false;
        
        // Add one initial seeder in the center
        addNode(true, canvas.width / 2, canvas.height / 2);
        
        // Add initial leechers randomly around it
        for(let i=0; i<5; i++) { addNode(false); }
    }

    function addNode(isSeeder = false, forceX = null, forceY = null) {
        if (nodes.length >= maxNodes) return;
        
        const id = nodes.length;
        const padding = 60;
        const x = forceX || (padding + Math.random() * (canvas.width - padding * 2));
        const y = forceY || (padding + Math.random() * (canvas.height - padding * 2));
        
        const newNode = new Node(id, x, y);
        if (isSeeder) {
            newNode.status = 'full';
            newNode.chunks = newNode.maxChunks;
        }
        nodes.push(newNode);
        
        // Connect to existing mesh
        if (nodes.length > 1) {
            let availableNodes = [...nodes].filter(n => n.id !== newNode.id);
            // Sort by distance to connect to nearest neighbors physically
            availableNodes.sort((a, b) => {
                let distA = Math.hypot(a.x - newNode.x, a.y - newNode.y);
                let distB = Math.hypot(b.x - newNode.x, b.y - newNode.y);
                return distA - distB;
            });
            
            let numConnections = Math.min(Math.floor(Math.random() * 2) + 2, availableNodes.length);
            for(let i=0; i<numConnections; i++) {
                edges.push(new Edge(newNode, availableNodes[i]));
            }
        }
    }

    function findNeighbors(node) {
        let neighbors = [];
        edges.forEach(e => {
            if (e.node1 === node) neighbors.push(e.node2);
            if (e.node2 === node) neighbors.push(e.node1);
        });
        return neighbors;
    }

    function updateNetwork() {
        ctx.clearRect(0, 0, canvas.width, canvas.height);
        
        edges.forEach(e => e.draw());
        
        for (let i = packets.length - 1; i >= 0; i--) {
            let p = packets[i];
            p.update();
            p.draw();
            
            if (p.progress >= 1) {
                if (p.target.chunks < p.target.maxChunks) {
                    p.target.chunks++;
                    if (p.target.chunks === p.target.maxChunks) {
                        p.target.status = 'full';
                    } else {
                        p.target.status = 'partial';
                    }
                }
                packets.splice(i, 1);
            }
        }
        
        nodes.forEach(n => n.draw());
        
        if (isSharing && Math.random() < 0.15) {
            let senders = nodes.filter(n => n.chunks > 0);
            if (senders.length > 0) {
                let sender = senders[Math.floor(Math.random() * senders.length)];
                let neighbors = findNeighbors(sender);
                let validTargets = neighbors.filter(n => n.chunks < n.maxChunks);
                
                if (validTargets.length > 0) {
                    let target = validTargets[Math.floor(Math.random() * validTargets.length)];
                    packets.push(new Packet(sender, target));
                }
            }
        }
        animationId = requestAnimationFrame(updateNetwork);
    }

    document.getElementById('addNodeBtn').addEventListener('click', () => addNode(false));
    document.getElementById('startSharingBtn').addEventListener('click', () => isSharing = true);
    document.getElementById('resetBtn').addEventListener('click', () => {
        cancelAnimationFrame(animationId);
        initNetwork();
        updateNetwork();
    });

    initNetwork();
    updateNetwork();
</script>
</body>
</html>
