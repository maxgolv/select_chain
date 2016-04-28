# select_chain
Зависимые списки (под Рево)

На странице должен быть вывод json вроде 
[{"id":"777","title":"Значение"},{"id":"778","title":"Значение"}]
//аяксом вытягиваем данные по селекту
function ajaxselect(value,target) { 
    $.ajax({
        url: "/katalog",
        dataType: 'json',
        type: 'GET',
        data: {'parent': value}
    }).done(function (data) { //получаем json со страницы по гет-параметру
        if(data.length !== 0){
            $('select[name="'+target+'"] option:gt(0)').remove(); //убираем лишнее
            for(var i=0;i<data.length;i++){ //заполняем
                $('<option data-value="'+data[i]["id"]+'"value="'+data[i]["title"]+'">'+data[i]["title"]+'</option>').appendTo('select[name="'+target+'"]');
            }
        }
    });
}


$(document).ready(function() {
    $('select.ajax_chain').change(function(){
        var value = $(this).find('option:selected').data("value");  //получаем id для аякса
        var target= $(this).data("change");  //получаем атрибут name селекта, который будем изменять
        if(value){
            ajaxselect(value,target);
        }
    });

});
