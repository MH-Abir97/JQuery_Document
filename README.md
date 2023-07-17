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
        });


     
      
    });

   

    let your_array = [];
    ## Save Data with Table List
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

    $(".PasswordId").change(function () {
        var value = $(this).val();
        var id = $(this).attr('id');
        console.log(value + " " + id);
    });
    ## Remopve Data with Table List
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
       
    });
});









    
