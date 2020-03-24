<!DOCTYPE html>
<html>
    <head>
        <meta charset="utf-8">
        <title>СибирскийХард+</title>
        <style>
            * {
                font-family: Arial, Helvetica, sans-serif;
                margin-left: 25px;
            }
            p {
                margin-top: 0;
                margin-bottom: 0;
            }
            #input {
                margin-bottom: 25px;
            }
            #process {
                margin-left: 0;
            }
            #result {
                width: 500px;
            }
        </style>
        <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.4.1/jquery.min.js"></script>
    </head>
    <body>
        <p>Шифротекст:</p>
        <input id="input" type="text"></input>
        <button id="process">Расшифровать</button>
        <p>Текст:</p>
        <p id="result">*Здесь появится расшифрованный текст*</p>

        <script>
            $("#process").click(function () {
                var input = $("#input").val();
                
                var no_spaces = input.split("").map(function (value, index, array) {
                    if ((index + 1) % 5 != 0) {
                        return value;
                    }
                }).join("");

                var stairs = [];
                var x = 0, y = 0;
                var stage = 0;
                for (var i = 0; i < no_spaces.length; i++) {
                    if (stairs[y] == undefined) {
                        stairs.push([]);
                    }
                    if (stairs[y][x] == undefined) {
                        stairs[y].push(i+1);
                    }

                    if (stage == 0) {
                        x++;
                        stage = 1;
                    }
                    else if (stage == 1) {
                        x--;
                        y++;
                        if (x == 0) {
                            stage = 2;
                        }
                    }
                    else if (stage == 2) {
                        y++;
                        stage = 3;
                    }
                    else if (stage == 3) {
                        x++;
                        y--;
                        if (y == 0) {
                            stage = 0;
                        }
                    }
                }

                result = "";
                x = 0, y = 0;
                stage = 0;
                for (var i = 0; i < no_spaces.length; i++) {
                    stairs_pos = 0;
                    for (var j = 0; j < y; j++) {
                        stairs_pos += stairs[j].length;
                    }
                    stairs_pos += x;

                    result += no_spaces[stairs_pos];

                    if (stage == 0) {
                        x++;
                        stage = 1;
                    }
                    else if (stage == 1) {
                        x--;
                        y++;
                        if (x == 0) {
                            stage = 2;
                        }
                    }
                    else if (stage == 2) {
                        y++;
                        stage = 3;
                    }
                    else if (stage == 3) {
                        x++;
                        y--;
                        if (y == 0) {
                            stage = 0;
                        }
                    }
                }

                $("#result").html(result);
            });
        </script>
    </body>
</html>