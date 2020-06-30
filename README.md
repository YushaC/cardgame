<html>

<head>

    <style type="text/css">
        body {
            background: white;
            font-family: Tahoma;
            color: #666666;
            margin: 0px 0px 0px 0px;
            font-size: 0.9em;
            text-align: center;
            text-align: left;
            width: 100%;
            height: auto;
            height: 100%;
            min-width: 1024px;
        }

        #title {
            background-color: #E1E1E1;
            width: 100%;
            overflow: hidden;
            border: 1px solid #e0e0e0;
            border-top: 0px;
            border-left: 0px;
            border-right: 0px;
            background-color: rgba(0, 0, 0, .03);
            box-shadow: 0 1px 6px rgba(0, 0, 0, .08);
            height: 90px;
            min-height: 60px;
            text-align: center;
        }

        #titleInside {
            margin: auto;
            width: 1024px;
            height: auto;
            position: relative;
            font-size: 2em;
            padding-left: 60px;
            padding-top: 13px;
        }

        #content {
            width: 100%;
            overflow: hidden;
            border: 1px solid #e0e0e0;
            border-top: 0px;
            border-left: 0px;
            border-right: 0px;
            border-bottom: 0px;
        }

        #contentInside {
            margin: auto;
            width: 1024px;
            height: auto;
            position: relative;
            padding: 20px;
            font-size: 2em;
            padding-left: 60px;
        }

        .card {
            width: 155px;
            height: 190px;
            background-color: #E1E1E1;
            float: left;
            margin: 5px;
        }

        #titleInside img {
            float: left;
        }

        #fails {
            float: left;
            border: 1px solid #e0e0e0;
            background-color: white;
            font-size: 15px;
            padding: 6px;
            margin-top: 30px;
            margin-left: 20px;
            background: #f7f7f7;
            /* Old browsers */
            background: -moz-linear-gradient(top, #f7f7f7 0%, #ffffff 100%);
            /* FF3.6+ */
            background: -webkit-gradient(linear, left top, left bottom, color-stop(0%, #f7f7f7), color-stop(100%, #ffffff));
            /* Chrome,Safari4+ */
            background: -webkit-linear-gradient(top, #f7f7f7 0%, #ffffff 100%);
            /* Chrome10+,Safari5.1+ */
            background: -o-linear-gradient(top, #f7f7f7 0%, #ffffff 100%);
            /* Opera 11.10+ */
            background: -ms-linear-gradient(top, #f7f7f7 0%, #ffffff 100%);
            /* IE10+ */
            background: linear-gradient(to bottom, #f7f7f7 0%, #ffffff 100%);
            /* W3C */
            filter: progid:DXImageTransform.Microsoft.gradient(startColorstr='#f7f7f7', endColorstr='#ffffff', GradientType=0);
            /* IE6-9 */

        }
    </style>

    <script type="text/javascript" src="jquery-1.9.1.js"></script>
    <script src="http://code.jquery.com/jquery-migrate-1.1.1.js"></script>
    <script type="text/javascript">
        var containerTest = 0;
        var before = null;
        var imageSelected;
        var containerFails = 0;
        var containerCertain = 0;
        var arrayImagenes = ["IMAGENES/bedfox.jpg", "IMAGENES/bookfox.jpg", "IMAGENES/grassfox.jpg",
            "IMAGENES/handfox.jpg", "IMAGENES/handpard.jpg", "IMAGENES/leopard.jpg", "IMAGENES/meow.jpg",
            "IMAGENES/pinkfox.jpg", "IMAGENES/meow.jpg"
        ];
        var qualityImagenes = arrayImagenes.length;
        var arrayPositiones = new Array(qualityImagenes);
        $(document).ready(function () {
            //Create array position
            var containerPositiones = 0;
            while (containerPositiones < qualityImagenes * 2) {
                var imagenPut = Math.floor((Math.random() * qualityImagenes));
                var containerPositionesRepeated = 0;
                for (var x = 0; x < containerPositiones; x++) {
                    if (arrayPositiones[x] == imagenPut) containerPositionesRepeated++;
                }
                if (containerPositionesRepeated < 2) {
                    arrayPositiones[containerPositiones] = imagenPut;
                    containerPositiones++;
                }
            }

            //Action after a click
            $("td").click(function () {
                containerTest++;
                //Select a card box
                var box = $(this).attr("id");
                if (containerTest > 1) {
                    imageSelected = arrayPositiones[box];
                    $("#" + box).animate({
                        width: "toggle",
                        opacity: "toggle"
                    }, 500);
                    $("#" + box).animate({
                        width: "toggle",
                        opacity: "toggle"
                    }, 500);
                    window.setTimeout(function () {
                        $("#" + box).css("background", "url(" + arrayImagenes[
                            imageSelected] + ")");
                    }, 500);
                    if (arrayPositiones[box] != arrayPositiones[before]) {
                        containerFails++;
                        $("#failsN").html(containerFails);
                        window.setTimeout(function () {
                            $("#" + box).animate({
                                width: "toggle",
                                opacity: "toggle"
                            }, 500);
                            $("#" + box).animate({
                                width: "toggle",
                                opacity: "toggle"
                            }, 500);
                            $("#" + before).animate({
                                width: "toggle",
                                opacity: "toggle"
                            }, 500);
                            $("#" + before).animate({
                                width: "toggle",
                                opacity: "toggle"
                            }, 500);
                            window.setTimeout(function () {
                                $("#" + box).css("background", "");
                                $("#" + before).css("background", "");
                            }, 500);
                        }, 1000);
                    } else {
                        containerCertain++;
                        $("#certain").html(containerCertain);
                    }
                    containerTest = 0;

                } else {
                    before = box;
                    imageSelected = arrayPositiones[box];
                    $("#" + box).animate({
                        width: "toggle",
                        opacity: "toggle"
                    }, 500);
                    $("#" + box).animate({
                        width: "toggle",
                        opacity: "toggle"
                    }, 500);
                    window.setTimeout(function () {
                        $("#" + box).css("background", "url(" + arrayImagenes[
                            imageSelected] + ")");
                    }, 500);
                    containerTest++;
                }
            })
        });
    </script>

</head>

<body>
    <div id="title">
        <div id="titleInside">
            <img src="IMAGENES/titulo.png">
            <div id="fails">配對失敗: <span id="failsN">0</span></div>
            <div id="fails">配對成功: <span id="certain">0</span></div>
        </div>
    </div>
    <div id="content">
        <div id="contentInside">
            <table>
                <tr>
                    <td class="card" id="0"></td>
                    <td class="card" id="1"></td>
                    <td class="card" id="2"></td>
                    <td class="card" id="3"></td>
                    <td class="card" id="4"></td>
                    <td class="card" id="5"></td>
                </tr>
                <tr>
                    <td class="card" id="6"></td>
                    <td class="card" id="7"></td>
                    <td class="card" id="8"></td>
                    <td class="card" id="9"></td>
                    <td class="card" id="10"></td>
                    <td class="card" id="11"></td>
                </tr>
                <tr>
                    <td class="card" id="12"></td>
                    <td class="card" id="13"></td>
                    <td class="card" id="14"></td>
                    <td class="card" id="15"></td>
                    <td class="card" id="16"></td>
                    <td class="card" id="17"></td>
                </tr>
            </table>
        </div>
    </div>
</body>
<html>
