Between rd-132211-launcher and 0.0.12a_03-200018 the world is stored in a gzipped file called "level.dat".

The file is a list of block IDs, each one being a byte. Blocks are stored starting at 0,0,0 going in the x, z and y directions (starting at the front-left-bottom corner going left-to-right, front-to-back and bottom-to-top based on the spawning angle).

In rd-132211-launcher and rd-132328-launcher an ID `01` indicated the existance of a block and any other ID is interpreted as the lack of a block.

In rd-160052-launcher and later the type of block is determined by the block ID.

<style>table,th,td{border:1px solid black;border-collapse:collapse;text-align:center;padding-left:4px;padding-right:4px;}</style>
<table>
  <tr>
    <th>ID</th>
    <th>Block</th>
    <th>Version added</th>
  </tr>
  <tr>
    <td><code>01</code></td>
    <td>rock</td>
    <td>rd-160052-launcher</td>
  </tr>
  <tr>
    <td><code>02</code></td>
    <td>grass</td>
    <td>rd-160052-launcher</td>
  </tr>
  <tr>
    <td><code>03</code></td>
    <td>dirt</td>
    <td>rd-160052-launcher</td>
  </tr>
  <tr>
    <td><code>04</code></td>
    <td>stoneBrick</td>
    <td>rd-160052-launcher</td>
  </tr>
  <tr>
    <td><code>05</code></td>
    <td>wood</td>
    <td>rd-160052-launcher</td>
  </tr>
  <tr>
    <td><code>06</code></td>
    <td>bush</td>
    <td>rd-161348-launcher</td>
  </tr>
  <tr>
    <td><code>07</code></td>
    <td>unbreakable</td>
    <td>0.0.12a_03-200018</td>
  </tr>
  <tr>
    <td><code>08</code></td>
    <td>water</td>
    <td>0.0.12a_03-200018</td>
  </tr>
  <tr>
    <td><code>09</code></td>
    <td>calmWater</td>
    <td>0.0.12a_03-200018</td>
  </tr>
  <tr>
    <td><code>0A</code></td>
    <td>lava</td>
    <td>0.0.12a_03-200018</td>
  </tr>
  <tr>
    <td><code>0B</code></td>
    <td>calmLava</td>
    <td>0.0.12a_03-200018</td>
  </tr>
</table>