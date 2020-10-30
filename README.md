## Simple Gantt chart in R

#### Code

<div id="code-element"></div>
<script src="https://unpkg.com/axios/dist/axios.min.js"></script>
<script>
      axios({
      method: 'get',
      url: 'https://github.com/andrewmarx/gantt/gantt.R'
       })
      .then(function (response) {
         document.getElementById("code-element").innerHTML = response.data;
      });
</script>

#### Output

![]("gantt.png")
