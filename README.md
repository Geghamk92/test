<!DOCTYPE html>
<html>
    <head>
        <title>test</title>
        <style>
        #create_tb {
            background-color: slategrey;
            padding: 5px 10px;
            color: white;
        }
        .container_for_buttons{
            position: relative;
            padding-bottom: 20px;
        }
        .container_for_buttons button {
            padding: 5px;
            margin: 0px 4px;
            background-color: silver;
            font-size: 15px;
        }
        .th {
            background-color: navy;
            padding: 5px 30px;
            color: white;
        }
        tr:nth-child(even){
            background-color: #f2f2f2;
            height: 20px;
        }
        tr:nth-child(odd){
            background-color: lightslategray;
            color: white;
            height: 20px;
        }
        </style>
    </head>
    <body>
        <div class="main_div">
        <button id="create_tb">Создать таблицу</button>
        <br /><br />
        <p id="json"></p>
        <br /><br />
        <script>
        //создать конструктр table (начало)
        function Table_cons(fields, rows, meta){
                var div_for_buttons = document.createElement("div");
                document.body.appendChild(div_for_buttons);
                var cr_table = document.createElement("table");
                var main_div = document.getElementsByClassName("main_div");
                var div_for_table = document.createElement("div");
                main_div[0].appendChild(div_for_buttons);
                main_div[0].appendChild(div_for_table);
                div_for_table.appendChild(cr_table);
                //div_for_table.appendChild(cr_table);
                
                if(!Array.isArray(meta)) alert("В качестве третьего параметра передайте css-классы");
                
                else if(Array.isArray(meta)) {
                    //Создать tr-и по заданным параметрам(начало)
                    for(var i = 0; i < rows; i++){
                        
                        var cr_tr = cr_table.insertRow(0);
                        
                        if(i % 2 == 0){
                             cr_tr.className = meta[1];
                        }//канец if-а
                        else {
                             cr_tr.className = meta[2]
                        }//канец else-а
                       
                       //Создать th-и по заданным параметрам(начало)
                        if(i == (rows-1)){

                            for(var e = 0; e < fields.length; e++){
                               var cr_th = document.createElement("th");
                               cr_tr.appendChild(cr_th);
                               cr_th.innerHTML = fields[e];
                               cr_th.className = meta[0];
                            }//канец for-а
                        
                        }//канец if-а
                        //Создать th-и по заданным параметрам(канец)

                        //Создать td-и по заданным параметрам(начало)
                        else{

                            for(var j = 0; j < fields.length; j++){
                               var cr_td = cr_tr.insertCell(j);
                               cr_td.innerHTML = "Hello";
                            }//канец for-а

                        }//канец else-а
                        //Создать td-и по заданным параметрам(канец)

                    }//Создать tr-и по заданным параметрам(канец)
                
                    //Повесить обработчик события dblclick для создании input area на table (начало)
                    cr_table.addEventListener("dblclick", cr_input_area);
                    function cr_input_area(event){
                              var target = event.target;
                              
                              while(target.tagName != "TABLE"){
                                 
                                 if(target.tagName == "TD"){
                                    var w = target;
                                    var input = document.createElement("input");
                                    input.setAttribute("type", "text");
                                   
                                    //если input area уже создан то input.value = input.value
                                    if(w.children[0]){
                                        input.setAttribute("value", target.children[0].value);
                                    }
                                    //если input area уже создан то input.value = td.innerHTML
                                    else {
                                        input.setAttribute("value", target.innerHTML);
                                    }
                                    
                                    target.innerHTML = "";
                                    target.appendChild(input);
                                    
                                    //создать кнопка для сохранение значение input-а (начало)
                                    var button = document.createElement("button");
                                    button.innerHTML = "Save";
                                    target.appendChild(button);
                                    button.onclick = function(){
                                        var x = document.getElementsByTagName("TD");
                                        w.innerHTML = input.value;
                                    }
                                    //создать кнопка для сохранение значение input-а (канец)

                                 }
                                 
                                 target = target.parentNode;
                              } 

                    }
                    //Повесить обработчик события dblclick для создании input area на table (канец)

                    //создать table (начало)
                    this.create_table = create_table_by_arguments;
                    function create_table_by_arguments(){                                                       
                        
                           //добавляет строку после указанной в параметре строки (начало)
                           var cr_butt_for_cr_tr_by_index = document.createElement("button");
                           cr_butt_for_cr_tr_by_index.innerHTML = "Добавить строку";
                           cr_butt_for_cr_tr_by_index.className = "butt_tr_by_index";
                        
                           function insert_row(){
                              var row_after_index = +prompt("vor indexic");
                              var new_tr_by_index = cr_table.insertRow(row_after_index + 1);
                              for(var k = 0; k < fields.length; k++){
                                 var td_for_new_tr_by_index = new_tr_by_index.insertCell(0);
                              }
                           }
                           //добавляет строку после указанной в параметре строки (канец)

                           //добавляет строку в конец таблицы (начало)
                           var cr_butt_for_cr_tr_end = document.createElement("button");
                           cr_butt_for_cr_tr_end.innerHTML = "Добавить строку в канце";
                           cr_butt_for_cr_tr_end.className = "butt_tr_end";

                           function add_row(){
                              var amount_tr = document.getElementsByTagName("TR");
                              var new_tr_in_end = cr_table.insertRow(amount_tr.length);
                              for(var k = 0; k < fields.length; k++){
                                 var td_for_new_tr_in_end = new_tr_in_end.insertCell(0);
                              }
                           }
                           //добавляет строку в конец таблицы (канец)

                           //очищает таблицу от данных (начало)
                           var cr_butt_for_clean_all_td = document.createElement("button");
                           cr_butt_for_clean_all_td.innerHTML = "Очищать таблица";
                           cr_butt_for_clean_all_td.className = "butt_clean_all_td";                       

                           function clean_table(){
                              var td_clean = document.getElementsByTagName("TD");
                              for(var cl = 0; cl < td_clean.length; cl++){
                                  td_clean[cl].innerHTML = "";
                              }
                           }
                           //очищает таблицу от данных (канец)

                           //получает JSON объект данных из таблицы (начало)
                           var cr_butt_for_get_json_obj = document.createElement("button");
                           cr_butt_for_get_json_obj.innerHTML = "Получит JSON обект";
                           cr_butt_for_get_json_obj.className = "butt_get_json_obj";

                           function get_data() {

                               var obj_0 = {
                                              "th_1": "hello_1",
                                              "th_2": "hello_2",
                                              "th_3": "hello_3"
                                           }
                              var table_json = [];
                                    for(var h = 0; h < (rows - 1); h++){
                                        table_json[h] = obj_0;
                                    }
   
                               var col = [];
                               for (var i = 0; i < table_json.length; i++) {
                                  for (var key in table_json[i]) {
                                      if (col.indexOf(key) === -1) {
                                          col.push(key);
                                      }
                                  }
                               }

                               var my_table = document.createElement("table");


                               var tr = my_table.insertRow(-1);                   

                               for (var i = 0; i < col.length; i++) {
                                  var th = document.createElement("th");
                                  th.className = "th";     
                                  th.innerHTML = col[i];
                                  tr.appendChild(th);
                               }

                               for (var i = 0; i < table_json.length; i++) {

                               tr = my_table.insertRow(-1);

                              for (var j = 0; j < col.length; j++) {
                                 var cell = tr.insertCell(-1);
                                 cell.innerHTML = table_json[i][col[j]];
                              }
                           }

                            div_for_table.innerHTML = "";
                            div_for_table.appendChild(my_table);
                         }
                         //получает JSON объект данных из таблицы (канец)

                           //добавить кнопки в div и повесить обработчик события (начало)
                           div_for_buttons.className = "container_for_buttons";
                           div_for_buttons.appendChild(cr_butt_for_cr_tr_by_index);
                           div_for_buttons.appendChild(cr_butt_for_cr_tr_end);
                           div_for_buttons.appendChild(cr_butt_for_clean_all_td);
                           div_for_buttons.appendChild(cr_butt_for_get_json_obj);
                           div_for_buttons.onclick = function(event){
                               var target_butt = event.target;

                               if(target_butt.className == "butt_tr_by_index"){
                                   insert_row();
                               }
                               else if(target_butt.className == "butt_tr_end"){
                                   add_row();
                               }
                               else if(target_butt.className == "butt_clean_all_td"){
                                   clean_table();
                               }
                               else if(target_butt.className == "butt_get_json_obj"){
                                   get_data();
                               }
                           }//добавить кнопки в div и повесить обработчик события (канец)

                    }//создать table (канец)
                                       
                }//конец else-a
        
        }//создать конструктр table (канец)
        
        //найти кнопку, повесить обр. события, получить параметры, создать объект, вызвать функцию для создания table (начало)
        var button_cr_tb = document.getElementById("create_tb");
        button_cr_tb.addEventListener("click", create_table_obj);
        function create_table_obj(){
            var headings = prompt("Запишите заголовки для столбцов, разделяя запятыми");
            var arr_headings = headings.split(",");
            var amount_row = +prompt("Напишите количество строк");
            
            if(!isNaN(parseFloat(amount_row)) && isFinite(amount_row) && (amount_row >= 0)){
                  var obj = new Table_cons(arr_headings, amount_row, ["th", "tr:nth-child(even)", "tr:nth-child(odd)"]);
                  obj.create_table();
                  button_cr_tb.removeEventListener("click", create_table_obj);
            }
            else alert("Количество строк должен быть число больше нуля");

        };
        //найти кнопку, повесить обр. события, получить параметры, создать объект, вызвать функцию для создания table (канец)
        </script>
        </div>
    </body>
</html>
