
<link href="https://cdnjs.cloudflare.com/ajax/libs/bootstrap-multiselect/0.9.13/css/bootstrap-multiselect.css" rel="stylesheet" />
<script src="https://cdnjs.cloudflare.com/ajax/libs/bootstrap-multiselect/0.9.13/js/bootstrap-multiselect.js"></script>

// for multiselect
$(document).ready(function(){  
        $('#Employeelist').multiselect({
                includeSelectAllOption: true
            });
        $('#viewselect').click(function () {
            var selected = $("#example-getting-started option:selected");
                    var message = "";
                    selected.each(function () {
                        message += $(this).text() + " " + $(this).val() + "\n";
                    });
                    alert(message);
                });


});

 <div class="form-group">
   <label for="Date" class="col-lg-4 col-sm-4 control-label">Select Employees</label>
    <div class="col-md-8">
<select id="Employeelist" multiple="multiple" class="form-control"></select>
  <button class="btn btn-warning" type="button" id="viewselect">Add</button>
  </div>
  </div>
  
  
  /// Important Note when Populating employee list dynamically add the following code in after adding list items 
   ///Add   $('#example-getting-started').multiselect('rebuild');  very important other wise data will not get in display in select
  
  function Load_Supervisor_Employees_List_By_ID()
{
    $.ajax({
        type: "POST",
        dataType: 'json',
        url: "/ManageLeaves/Supervisor_Employees_List_By_ID",
        data: { SupervisorID: 3 },
        success: function (data) {
          
            var json = JSON.parse(JSON.stringify(data.msg))
           // alert(json[0].EmpID);
            var listItems="";
           // var listItems = "<option value=''>Select</option>";
         //   var json = JSON.parse(JSON.stringify(data.msg))
            for (var i = 0; i < json.length; i++) {
                listItems += "<option value='" + json[i].EmpID + "'>" + json[i].FirstName + "</option>";
            }
           
            $("#example-getting-started").html(listItems);
            $('#example-getting-started').multiselect('rebuild');
           },
        error: function () {
            console.log('Ajax Request Cannot Be Completed Sucessfully. Cannot Bind Data');
        }
    });
  
}
