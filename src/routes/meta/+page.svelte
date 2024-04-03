<script>
  // import * as d3 from "d3";
  // import { onMount } from "svelte";
  // import Pie from "$lib/Pie.svelte";

  // let data = [];
  // let commits = [];
  // let margin = { top: 10, right: 10, bottom: 30, left: 20 };
  // let cursor = { x: 0, y: 0 };
  // let svg;
  // let brushSelection;
  // let selectedLines;

  // let width = 1000,
  //   height = 600;

  // let usableArea = {
  //   top: margin.top,
  //   right: width - margin.right,
  //   bottom: height - margin.bottom,
  //   left: margin.left,
  // };
  // usableArea.width = usableArea.right - usableArea.left;
  // usableArea.height = usableArea.bottom - usableArea.top;

  // let yAxisGridlines;

  // function brushed(evt) {
  //   console.log(evt);
  //   brushSelection = evt.selection;
  // }

  // function isCommitSelected(commit) {
  //   if (!brushSelection) {
  //     return false;
  //   }

  //   let min = { x: brushSelection[0][0], y: brushSelection[0][1] };
  //   let max = { x: brushSelection[1][0], y: brushSelection[1][1] };
  //   let x = xScale(commit.date);
  //   let y = yScale(commit.hourFrac);
  //   return x >= min.x && x <= max.x && y >= min.y && y <= max.y;
  // }

  // onMount(async () => {
  //   data = await d3.csv("loc.csv", (row) => ({
  //     ...row,
  //     line: Number(row.line), // or just +row.line
  //     depth: Number(row.depth),
  //     length: Number(row.length),
  //     date: new Date(row.date + "T00:00" + row.timezone),
  //     datetime: new Date(row.datetime),
  //   }));

  //   commits = d3
  //     .groups(data, (d) => d.commit)
  //     .map(([commit, lines]) => {
  //       let first = lines[0];
  //       let { author, date, time, timezone, datetime } = first;
  //       let ret = {
  //         id: commit,
  //         url: "https://github.com/madelineleano/my-portfolio" + commit,
  //         author,
  //         date,
  //         time,
  //         timezone,
  //         datetime,
  //         hourFrac: datetime.getHours() + datetime.getMinutes() / 60,
  //         totalLines: lines.length,
  //       };

  //       // Like ret.lines = lines
  //       // but non-enumerable so it doesn’t show up in JSON.stringify
  //       Object.defineProperty(ret, "lines", {
  //         value: lines,
  //         configurable: true,
  //         writable: true,
  //         enumerable: false,
  //       });

  //       return ret;
  //     });
  // });

  // $: yScale = d3
  //   .scaleLinear()
  //   .domain([0, 24])
  //   .range([usableArea.bottom, usableArea.top]);
  // $: xScale = d3
  //   .scaleTime()
  //   .domain(d3.extent(commits, (d) => d.datetime))
  //   .range([usableArea.left, usableArea.right])
  //   .nice();

  // let xAxis, yAxis;

  // $: {
  //   d3.select(xAxis).call(d3.axisBottom(xScale));
  //   d3.select(yAxis).call(
  //     d3
  //       .axisLeft(yScale)
  //       .tickFormat((d) => String(d % 24).padStart(2, "0") + ":00")
  //   );
  // }

  // $: {
  //   d3.select(yAxisGridlines).call(
  //     d3.axisLeft(yScale).tickFormat("").tickSize(-usableArea.width)
  //   );
  // }

  // let hoveredIndex = -1;
  // $: hoveredCommit = commits[hoveredIndex] ?? {};

  // $: {
  //   d3.select(svg).call(d3.brush().on("start brush end", brushed));
  //   d3.select(svg).selectAll(".dots, .overlay ~ *").raise();
  // }

  // $: selectedCommits = brushSelection ? commits.filter(isCommitSelected) : [];
  // $: hasSelection = brushSelection && selectedCommits.length > 0;
  // $: selectedLines = (hasSelection ? selectedCommits : commits).flatMap(
  //   (d) => d.lines
  // );
  // $: languageBreakdown = d3.rollup(selectedLines,  amount => amount.length, lang => lang.type);
</script>

<svelte:head>
  <title>Meta</title>
</svelte:head>

<h1>Meta</h1>
<!-- 
<dl
  id="commit-tooltip"
  class="info tooltip"
  hidden={hoveredIndex === -1}
  style="top: {cursor.y}px; left: {cursor.x}px"
>
  <dt>Commit</dt>
  <dd><a href={hoveredCommit.url} target="_blank">{hoveredCommit.id}</a></dd>

  <dt>Date</dt>
  <dd>{hoveredCommit.datetime?.toLocaleString("en", { date: "full" })}</dd>

  <dt>Author</dt>
  <dd>{hoveredCommit.author}</dd>
</dl>

<svg viewBox="0 0 {width} {height}" bind:this={svg}>
  <g transform="translate(0, {usableArea.bottom})" bind:this={xAxis} />
  <g
    class="gridlines"
    transform="translate({usableArea.left}, 0)"
    bind:this={yAxisGridlines}
  />

  <g transform="translate({usableArea.left}, 0)" bind:this={yAxis} />
  <g class="dots">
    {#each commits as commit, index}
      <circle
        class:selected={isCommitSelected(commit)}
        cx={xScale(commit.datetime)}
        cy={yScale(commit.hourFrac)}
        r="5"
        fill="steelblue"
        on:mouseenter={(evt) => {
          hoveredIndex = index;
          cursor = { x: evt.x, y: evt.y };
        }}
        on:mouseleave={(evt) => (hoveredIndex = -1)}
      />
    {/each}
  </g>
</svg>
<p>{hasSelection ? selectedCommits.length : "No"} commits selected</p>

{#each languageBreakdown as [language, lines] }
  <p>{language}: </p>
  <p> {Math.round((lines / selectedLines.length) * 100)}%</p>
{/each}

<Pie data = {Array.from(languageBreakdown).map(([language, lines]) => ({label: language, value: lines}))}/> -->

<dl class="stats">
  <dt>Total Lines of Code:</dt>
  <dd>{data.length}</dd>
  <dt>Total commits:</dt>
  <dd>{commits.length}</dd>
  <dt>Total Files:</dt>
  <dd>{d3.group(data, (d) => d.file).size}</dd>
  <dt>Average depth of line:</dt>
  <dd>{d3.mean(data, (d) => d.depth)}</dd>
  <dt>Maximum depth of line:</dt>
  <dd>{d3.max(data, (d) => d.depth)}</dd>
</dl>

<style>
  svg {
    overflow: visible;
  }

  .gridlines {
    stroke-opacity: 0.2;
  }

  dl.info {
    display: grid;
    transition-duration: 500ms;
    transition-property: opacity, visibility;

    &[hidden]:not(:hover, :focus-within) {
      opacity: 0;
      visibility: hidden;
    }
  }
  .selected {
    fill: red;
  }
  .tooltip {
    position: fixed;
    top: 1em;
    left: 1em;
    background-color: oklch(100% 0% 0 / 80%);
    border-radius: 3px;
    box-shadow: 10px 5px 5px grey;
    backdrop-filter: blur(2px);
  }

  circle {
    transition: 200ms;
    transform-origin: center;
    transform-box: fill-box;

    &:hover {
      transform: scale(1.5);
    }
  }
</style>
