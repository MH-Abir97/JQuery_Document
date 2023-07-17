# JQuery Necessary Document :
<div class="row">
        <div class="col-md-4">
            <div class="form-group">
                <input type="text" id="UserName" name="UserName" class="form-control" placeholder="User Name" />
            </div>
            <div class="form-group">
                <input type="text" id="Password" name="Password" class="form-control" placeholder="Password" />
            </div>
            
            <div class="row">
                <div class="col-md-10">
                </div>
                <div class="col-md-2">
                   <button id="btnAdd" class="btn btn-primary text-right">Add</button>
                </div>
            </div>
        </div>
        <div class="col-md-4">
            <table class="table table-bordered" >
                <thead>
                    <tr>
                        <th class="text-center">User Name </th>
                        <th class="text-center">Password </th>
                        <th class="text-center">Remove </th>
                    </tr>
                </thead>
                <tbody id="tbody" class="tbodyValue">
                </tbody>
            </table>
            <div class="row">
                <div class="col-md-10">
                </div>
                <div class="col-md-2">
                    <button id="SaveBtn" class="btn btn-success text-right">Save</button>
                </div>
            </div>
           
        </div>
    </div>


    $(document).ready(function () {
    var arrayList = [];
    var TempList = [];
    var rowIdx = 0;
    $("#btnAdd").click(function (e) {
        e.preventDefault();
        
        arrayList = [];
        var obj = {};
        obj.UserName = $("#UserName").val();
        obj.Password = $("#Password").val();
        rowIdx++;
        obj.Index = rowIdx;
     
        arrayList.push(obj);
        TempList.push(obj);
     //  var resultstring=""


        //for (i = 0; i < arrayList.length; i++) {
        //    $('#TableId').append('<td>' + arrayList[i].UserName + '</td>');
        //}

        //for (var j = 0; j < arrayList.length; j++) {
        //    resultstring += '<td></br>' + arrayList[j].UserName + '</td></br>';
        //}
        //$('#TableId').append(resultstring);


       // $('#TableId').append('</table>');
        //var rowIdx = 0;
        //for (var i = 0; i < arrayList.length; i++) {
           
        //}

       
        $.each(arrayList, function (key, value) {
            var tbody = `<tr> 
                     <td class="row-index text-center UserName">
                      ${value.UserName}
                       
                     </td>
                     <td class="row-index text-center">
                       <input type="text" class="form-control PasswordId" id='${value.Index}' value="${value.Password}"  name="Password"  placeholder="Password">
                     </td>
                     <td class="text-center">
                      <button class="btn btn-danger remove" type="button" id='${value.Index}' >Remove</button>
                     </td>
                    </tr>`;

                   $('#tbody').append(tbody);

            //$('#tbody').append(`<tr>
            // <td class="row-index text-center">
            //  ${value.UserName}
            // </td>
            //  <td class="text-center">
            //    <button class="btn btn-danger remove"
            //      type="button" id='${value.Index}' >Remove</button>
            //    </td>
            //  </tr>`);
        });


     
      
    });

   

    let your_array = [];

    $(document).on('click', '#SaveBtn', function () {

        var tableData = [];
        $('#tbody tr').each(function (row, tr) {
            //var rowData = {
            //    Password: $(tr).find('.PasswordId').val(),
            //    UserName: $(tr).find('.UserName').text(),
            //};
            //tableData.push(rowData);
     
            var Password = $(tr).find('.PasswordId').val();
            TempList.forEach(function (aData, index) {
                if (index == row) {
                    aData.Password = Password;
                }
                
            });

        });
        console.log(tableData);
      
    });


    //$("#SaveBtn").click(function (e) {
    //    e.preventDefault();

    //    TempList.forEach(function (aData) {
    //        console.log(aData);
    //    });
    //})

    //$(".remove").click(function (e) {
    //    e.preventDefault();
    //    var child = $(this).closest('tr').nextAll();
    //    var id = $(this).attr('id');
    //})

    // Denotes total number of rows
   // var rowIdx = 0;

    // jQuery button click event to add a row
    //$('#addBtn').on('click', function () {

    //    // Adding a row inside the tbody.
    //    $('#tbody').append(`<tr id="R${++rowIdx}">
    //         <td class="row-index text-center">
    //         Row ${rowIdx}
    //         </td>
    //          <td class="text-center">
    //            <button class="btn btn-danger remove"
    //              type="button" id='${rowIdx}' >Remove</button>
    //            </td>
    //          </tr>`);
    //});

    // jQuery button click event to remove a row.
    //$('.tbodyValue').on('change', '.PasswordId', function () {
      

    //});

    $(".PasswordId").change(function () {
        var value = $(this).val();
        var id = $(this).attr('id');
        console.log(value + " " + id);
    });

    $('#tbody').on('click', '.remove', function () {

        // Getting all the rows next to the row
        // containing the clicked button

        var child = $(this).closest('tr').nextAll();
        var id = $(this).attr('id');
        var temp = Number(id);

       
     
        // Remove Form List=====>>>

        var list = TempList.filter((aData) => aData.Index == temp);

        for (var i = 0; i < TempList.length; i++) {
            if (TempList[i].Index == temp) {
                var ind = TempList.indexOf(TempList[i]);
                TempList.splice(ind, 1);
            }
        }
       

    

        // Iterating across all the rows 
        // obtained to change the index
        //child.each(function () {

        //    // Getting <tr> id.
        //    var id = $(this).attr('id');

        //    // Getting the <p> inside the .row-index class.
        //    var idx = $(this).children('.row-index').children('p');

        //    // Gets the row number from <tr> id.
        //    var dig = parseInt(id.substring(1));

        //    // Modifying row index.
        //    idx.html(`Row ${dig - 1}`);

        //    // Modifying row id.
        //    $(this).attr('id', `R${dig - 1}`);
        //});

        // Removing the current row.
          $(this).closest('tr').remove();

        // Decreasing total number of rows by 1.
       // rowIdx--;
    });
});









    
