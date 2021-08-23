---
layout: default
---
<!doctype html>
<html lang="en">
<head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <link rel="stylesheet" href="https://code.jquery.com/ui/1.12.1/themes/base/jquery-ui.css">
    <script src="https://code.jquery.com/jquery-1.12.4.js"></script>
    <script src="https://code.jquery.com/ui/1.12.1/jquery-ui.js"></script>
    <style type="text/css">
        .content{
            width:350px;
            margin:40px auto;
        }
        h2{
            text-align: center;
        }  
    </style>
</head>


<body>
    <div class="content">
        <p>
            <label for="amount">Age range:</label>
            <input type="text" id="amount" readonly style="border:0; color:#f6931f; font-weight:bold;">
        </p>
        <div id="slider-range"></div>
        <p>
            <label for "population">ONS 2020 mid-year population estimate:</label>
            <input type="text" id="population" readonly style="border:0; color:#f6931f; font-weight:bold;">
    </div>
</body>

<script>
    $( function() {
        $( "#slider-range" ).slider({
            range: true,
            min: 0,
            max: 90,
            values: [ 0, 90],
            slide: function( event, ui ) {
                $( "#amount" ).val( "" + ui.values[ 0 ] + "-" + ui.values[ 1 ] )
               var popdata = [{"age":0,"population":7205},{"age":1,"population":7648},{"age":2,"population":7899},{"age":3,"population":8068},{"age":4,"population":8396}, 
{"age":5,"population":8315},{"age":6,"population":8276},{"age":7,"population":8491},{"age":8,"population":8853},{"age":9,"population":9200},{"age":10,"population":8601},{"age":11,"population":8371},{"age":12,"population":8666},{"age":13,"population":8461},{"age":14,"population":8156},{"age":15,"population":7943},{"age":16,"population":7888},{"age":17,"population":7660},{"age":18,"population":7617},{"age":19,"population":9594},{"age":20,"population":10009},{"age":21,"population":10365},{"age":22,"population":10101},{"age":23,"population":9820},{"age":24,"population":9450},{"age":25,"population":9390},{"age":26,"population":9264},{"age":27,"population":9092},{"age":28,"population":8826},{"age":29,"population":8769},{"age":30,"population":8431},{"age":31,"population":8027},{"age":32,"population":8007},{"age":33,"population":8374},{"age":34,"population":8580},{"age":35,"population":8909},{"age":36,"population":8855},{"age":37,"population":9250},{"age":38,"population":8826},{"age":39,"population":9122},{"age":40,"population":8859},{"age":41,"population":8910},{"age":42,"population":8355},{"age":43,"population":8361},{"age":44,"population":8012},{"age":45,"population":8424},{"age":46,"population":8789},{"age":47,"population":8979},{"age":48,"population":9319},{"age":49,"population":9419},{"age":50,"population":9390},{"age":51,"population":9415},{"age":52,"population":9576},{"age":53,"population":9584},{"age":54,"population":9811},{"age":55,"population":9694},{"age":56,"population":9631},{"age":57,"population":9427},{"age":58,"population":8952},{"age":59,"population":8552},{"age":60,"population":8359},{"age":61,"population":7891},{"age":62,"population":7703},{"age":63,"population":7409},{"age":64,"population":7095},{"age":65,"population":6869},{"age":66,"population":6715},{"age":67,"population":6639},{"age":68,"population":6279},{"age":69,"population":6649},{"age":70,"population":6749},{"age":71,"population":6846},{"age":72,"population":7261},{"age":73,"population":7532},{"age":74,"population":5868},{"age":75,"population":5953},{"age":76,"population":5749},{"age":77,"population":5305},{"age":78,"population":4587},{"age":79,"population":4035},{"age":80,"population":4086},{"age":81,"population":4056},{"age":82,"population":3668},{"age":83,"population":3475},{"age":84,"population":3248},{"age":85,"population":2906},{"age":86,"population":2527},{"age":87,"population":2260},{"age":88,"population":2107},{"age":89,"population":1791},{"age":90,"population":7029}];
                var filteredtotal = popdata.filter(({age}) => age >  (ui.values[0]-1))
                filteredtotal = filteredtotal.filter(({age}) => age <  ui.values[1]+1)
                var result= filteredtotal.reduce(function(prev, cur) {
                  return prev + cur.population;
                }, 0);
               $( "#population" ).val( result)
            }
        });
        $( "#amount" ).val( "" + $( "#slider-range" ).slider( "values", 0 ) + "-" + $( "#slider-range" ).slider( "values", 1 ) );
        $("#population").val("696880");
    });


</script>
</html>


[back](./)
