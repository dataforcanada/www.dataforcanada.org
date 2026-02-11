---
title: Infrastructure
sidebar:
  open: true
---

## High-Level Overview

{{< rawhtml >}}
<style>
  .land {
            fill: #ddd;
            stroke: #999;
            stroke-width: 0.5;
        }

        .graticule {
            fill: none;
            stroke: #ccc;
            stroke-width: 0.5;
        }

        .connection {
            fill: none;
            stroke-width: 1.5;
            opacity: 0.6;
        }

        .node {
            cursor: pointer;
            stroke: #fff;
            stroke-width: 1;
        }

        .tooltip {
            position: absolute;
            background: white;
            border: 1px solid #ccc;
            padding: 10px;
            pointer-events: none;
            opacity: 0;
            transition: opacity 0.2s;
            border-radius: 4px;
            box-shadow: 0 2px 4px rgba(0,0,0,0.2);
            max-width: 350px;
        }

        .tooltip.visible {
            opacity: 1;
        }

        .tooltip-title {
            font-weight: bold;
            margin-bottom: 5px;
        }

        .tooltip-detail {
            font-size: 14px;
            margin: 2px 0;
        }
</style>
<svg id="map"></svg>
    <div class="tooltip"></div>
    <script type="module">
        import * as d3 from 'https://cdn.jsdelivr.net/npm/d3@7/+esm';

        // Infrastructure nodes
        const nodes = [
            { 
                id: 'smart-node-01', 
                name: 'Smart Node 01', 
                location: 'Toronto, Ontario, Canada',
                coords: [-79.38, 43.65], 
                specs: '50Gbps / 50Gbps, 950GB Flash Storage',
                jurisdiction: 'Singapore',
                color: '#9966CC' 
            },
            { 
                id: 'vancouver', 
                name: 'Internet Archive Mirror', 
                location: 'Vancouver, Canada',
                coords: [-123.12, 49.28],
                protocol: 'HTTP',
                jurisdiction: 'USA',
                color: '#002147' 
            },
            { 
                id: 'source-cooperative-oregon', 
                name: 'Source Cooperative', 
                location: 'Oregon, USA',
                coords: [-122.68, 45.52],
                specs: 'AWS S3 (us-west-2)',
                protocol: 'HTTP',
                jurisdiction: 'USA',
                color: '#002147' 
            },
            { 
                id: 'r2', 
                name: 'Cloudflare R2', 
                location: 'Eastern North America',
                coords: [-73.94, 40.71],
                specs: 'Primary Object Storage',
                protocol: 'HTTP',
                jurisdiction: 'USA',
                color: '#002147' 
            },
            { 
                id: 'san-francisco', 
                name: 'The Internet Archive', 
                location: 'San Francisco, California, USA',
                coords: [-122.42, 37.77],
                protocol: 'HTTP',
                jurisdiction: 'USA',
                color: '#002147' 
            },
            { 
                id: 'vps-01', 
                name: 'VPS 01', 
                location: 'Manassas, Virginia, USA',
                coords: [-77.48, 38.75],
                specs: '2.5Gbps / 2.5Gbps, 512GB Flash Storage',
                protocol: 'HTTP & P2P',
                jurisdiction: 'Germany',
                color: '#FFCC00' 
            },
            { 
                id: 'smart-node-02', 
                name: 'Smart Node 02', 
                location: 'Amsterdam, Netherlands',
                coords: [4.90, 52.37],
                specs: '50Gbps / 50Gbps, 950GB Flash Storage',
                jurisdiction: 'Singapore',
                color: '#9966CC' 
            },
            { 
                id: 'smart-node-03', 
                name: 'Smart Node 03', 
                location: 'Amsterdam, Netherlands',
                coords: [4.90, 52.37],
                specs: '50Gbps / 50Gbps, 6TB HDD Storage',
                jurisdiction: 'Singapore',
                color: '#9966CC' 
            },
            { 
                id: 'geneva', 
                name: 'Zenodo', 
                location: 'Geneva, Switzerland',
                coords: [6.14, 46.20],
                specs: 'Replicated in Budapest',
                protocol: 'HTTP',
                jurisdiction: 'Switzerland',
                color: '#D52B1E' 
            },
            { 
                id: 'budapest', 
                name: 'Zenodo Mirror', 
                location: 'Budapest, Hungary',
                coords: [19.04, 47.50],
                protocol: 'HTTP',
                jurisdiction: 'Switzerland',
                color: '#D52B1E' 
            }
        ];

        // Connections between nodes
        const connections = [
            { source: 'smart-node-01', target: 'smart-node-02', color: '#9966CC' },
            { source: 'smart-node-01', target: 'smart-node-03', color: '#9966CC' },
            { source: 'san-francisco', target: 'vancouver', color: '#999' },
            { source: 'geneva', target: 'budapest', color: '#D52B1E' },
            { source: 'smart-node-01', target: 'source-cooperative-oregon', color: '#9966CC' },
            { source: 'smart-node-01', target: 'r2', color: '#9966CC' },
            { source: 'smart-node-01', target: 'geneva', color: '#9966CC' },
            { source: 'smart-node-01', target: 'san-francisco', color: '#9966CC' },
            { source: 'smart-node-01', target: 'vps-01', color: '#9966CC' },
            { source: 'smart-node-02', target: 'source-cooperative-oregon', color: '#9966CC' },
            { source: 'smart-node-02', target: 'r2', color: '#9966CC' },
            { source: 'smart-node-02', target: 'geneva', color: '#9966CC' },
            { source: 'smart-node-02', target: 'san-francisco', color: '#9966CC' },
            { source: 'smart-node-02', target: 'vps-01', color: '#9966CC' },
            { source: 'smart-node-03', target: 'source-cooperative-oregon', color: '#9966CC' },
            { source: 'smart-node-03', target: 'r2', color: '#9966CC' },
            { source: 'smart-node-03', target: 'geneva', color: '#9966CC' },
            { source: 'smart-node-03', target: 'san-francisco', color: '#9966CC' },
            { source: 'smart-node-03', target: 'vps-01', color: '#9966CC' },
            { source: 'vps-01', target: 'smart-node-02', color: '#FFCC00' },
            { source: 'vps-01', target: 'smart-node-03', color: '#FFCC00' },
            { source: 'vps-01', target: 'r2', color: '#FFCC00' },
            { source: 'vps-01', target: 'san-francisco', color: '#FFCC00' },
            { source: 'vps-01', target: 'source-cooperative-oregon', color: '#FFCC00' },
            { source: 'vps-01', target: 'geneva', color: '#FFCC00' }
        ];

        const width = 960;
        const height = 600;

        const svg = d3.select('#map')
            .attr('width', width)
            .attr('height', height);

        const projection = d3.geoNaturalEarth1()
            .scale(180)
            .translate([width / 2, height / 2]);

        const path = d3.geoPath().projection(projection);
        const graticule = d3.geoGraticule();

        const g = svg.append('g');

        // Draw graticule
        g.append('path')
            .datum(graticule)
            .attr('class', 'graticule')
            .attr('d', path);

        // Group nodes by location to handle overlapping
        const nodesByLocation = {};
        nodes.forEach(node => {
            const key = node.coords.join(',');
            if (!nodesByLocation[key]) {
                nodesByLocation[key] = [];
            }
            nodesByLocation[key].push(node);
        });

        // Calculate offsets for nodes at same location
        const nodeOffsets = {};
        Object.entries(nodesByLocation).forEach(([key, nodesAtLocation]) => {
            if (nodesAtLocation.length === 1) {
                nodeOffsets[nodesAtLocation[0].id] = { dx: 0, dy: 0 };
            } else {
                // Create circular offset pattern for multiple nodes
                const radius = 8;
                nodesAtLocation.forEach((node, i) => {
                    const angle = (i / nodesAtLocation.length) * 2 * Math.PI;
                    nodeOffsets[node.id] = {
                        dx: Math.cos(angle) * radius,
                        dy: Math.sin(angle) * radius
                    };
                });
            }
        });

        // Tooltip
        const tooltip = d3.select('.tooltip');

        function showTooltip(event, nodesAtLocation) {
            let html = '';
            nodesAtLocation.forEach((node, i) => {
                if (i > 0) html += '<hr style="margin: 8px 0; border: none; border-top: 1px solid #ccc;">';
                html += `<div class="tooltip-title">${node.name}</div>`;
                html += `<div class="tooltip-detail">Location: ${node.location}</div>`;
                if (node.specs) html += `<div class="tooltip-detail">Specs: ${node.specs}</div>`;
                if (node.protocol) html += `<div class="tooltip-detail">Protocol: ${node.protocol}</div>`;
                html += `<div class="tooltip-detail">Jurisdiction: ${node.jurisdiction}</div>`;
            });
            
            tooltip
                .html(html)
                .classed('visible', true)
                .style('left', (event.pageX + 15) + 'px')
                .style('top', (event.pageY + 15) + 'px');
        }

        function hideTooltip() {
            tooltip.classed('visible', false);
        }

        // Load world map (GeoJSON)
        d3.json('https://raw.githubusercontent.com/nvkelso/natural-earth-vector/master/geojson/ne_110m_land.geojson').then(landData => {
            // Draw land
            g.append('g')
                .selectAll('path')
                .data(landData.features)
                .enter().append('path')
                .attr('class', 'land')
                .attr('d', path);

            // Draw connections
            const connectionGroup = g.append('g');
            connections.forEach(conn => {
                const source = nodes.find(n => n.id === conn.source);
                const target = nodes.find(n => n.id === conn.target);
                if (source && target) {
                    connectionGroup.append('path')
                        .datum({
                            type: 'LineString',
                            coordinates: [source.coords, target.coords]
                        })
                        .attr('class', 'connection')
                        .attr('d', path)
                        .attr('stroke', conn.color);
                }
            });

            // Draw nodes with offsets for overlapping positions
            const nodeGroup = g.append('g');
            
            // Draw each node with its offset
            nodes.forEach(node => {
                const coords = projection(node.coords);
                const offset = nodeOffsets[node.id];
                const locationKey = node.coords.join(',');
                const nodesAtThisLocation = nodesByLocation[locationKey];
                
                nodeGroup.append('circle')
                    .attr('class', 'node')
                    .attr('cx', coords[0] + offset.dx)
                    .attr('cy', coords[1] + offset.dy)
                    .attr('r', 4)
                    .attr('fill', node.color)
                    .on('mouseover', (event) => showTooltip(event, nodesAtThisLocation))
                    .on('mouseout', hideTooltip)
                    .on('mousemove', (event) => {
                        tooltip
                            .style('left', (event.pageX + 15) + 'px')
                            .style('top', (event.pageY + 15) + 'px');
                    });
            });
        });
    </script>
{{< /rawhtml >}}

## Infrastructure & Operating Costs

| Service | Description | CAD | USD | EUR |
| :--- | :--- | :--- | :--- | :--- |
| **CDN** | [CDN - Cloudflare Details](https://www.cloudflare.com/plans/) - WAF, CDN (Amortized Annual) | $30.90 | $22.60 | €19.13 |
| **CDN Services** | [Object Storage - Cloudflare Details](https://www.cloudflare.com/products/r2/) & [Serverless - Cloudflare Details](https://www.cloudflare.com/en-ca/plans/developer-platform/) (Variable) | $32.71 | $23.93 | €20.26 |
| **Smart Node 01** | [Decentralized Distribution - SlashN Services Details](https://ultra.cc/#plan-pricing) - Dedicated <abbr title="Peer-to-Peer">P2P</abbr> client | $28.98 | $21.21 | €17.95 |
| **Smart Node 02** | [Decentralized Distribution - SlashN Services Details](https://ultra.cc/#plan-pricing) - Dedicated <abbr title="Peer-to-Peer">P2P</abbr> client | $28.98 | $21.21 | €17.95 |
| **Smart Node 03** | [Decentralized Distribution - SlashN Services Details](https://ultra.cc/#plan-pricing) - Dedicated <abbr title="Peer-to-Peer">P2P</abbr> client | $27.31 | $20.13 | €16.95 |
| **VPS 01** | [Geospatial Services - Netcup Details](https://www.netcup.com/en/server/root-server) - ARM64 | $14.64 | $10.72 | €9.07 |
| **TOTAL** | **Monthly Run Rate** | **$163.52** | **$119.80** | **€101.31** |

**Note:** Currency conversions are based on rates from February 16, 2026.

## Roadmap: Resilience & Transparency

To support our mission of providing high-performance, analysis-ready data, we are currently developing a suite of public tools to make this distributed ecosystem more **FAIR** (Findable, Accessible, Interoperable, Reusable), **resilient**, and **transparent**.

These planned features are designed to help researchers and automated systems coordinate data access across the various platforms and mirrors we utilize.

### 1. Real-Time Service Status

We are building a comprehensive status dashboard that monitors the availability of the diverse storage locations we rely on, from our own Smart Nodes to external providers like the Internet Archive, Source Cooperative, and Zenodo. Users will be able to verify if a specific mirror is operational before initiating workflows.

### 2. Traffic & Load Optimization Statistics

To foster better cooperation between our systems and downstream users, we plan to expose traffic and connectivity statistics where possible.

This transparency allows automated systems to be "smart" about data retrieval. For example, a system could query these statistics to schedule bandwidth-intensive HTTP downloads during non-peak hours, or adjust behavior based on current connectivity loads during high-traffic periods of the workday. This improves performance for individual users while respecting the bandwidth constraints of the various host providers.

### 3. Community Issue Reporting

We are introducing a streamlined method for users to report access issues across any of the services we aggregate. By allowing the community to flag connectivity drops or data integrity issues quickly, we can identify bottlenecks or outages at specific providers and route users to alternative sources more effectively.
