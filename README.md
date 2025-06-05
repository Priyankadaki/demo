# demo
 public JsonResult SubmtStudentDetails(string Email = "", string Name = "", string Mobile = "", string State = "", string StudentId = "")
 {

     objModel.Name = `Name`;
     objModel.Email = Email;
     objModel.Phone = Mobile;
     objModel.modename = "insert";

     if (StudentId != null && StudentId != "0" && StudentId!="")
     {
         objModel.modename = "update";
         objModel.Id = Convert.ToInt32(StudentId); ;
     }
     DataSet ds_State = _studentBal.Student(objModel);

     if (ds_State != null && ds_State.Tables.Count > 0 && ds_State.Tables[0].Rows.Count > 0)
     {
         string dbMessage = ds_State.Tables[0].Rows[0]["message"].ToString(); 
         HttpContext.Session.SetString("successMsg", dbMessage);
     }
     else
     {
         HttpContext.Session.SetString("errorMsg", "Operation failed or returned no data.");
     }

     var successMsg = HttpContext.Session.GetString("successMsg") ?? string.Empty;
     var errorMsg = HttpContext.Session.GetString("errorMsg") ?? string.Empty;

     return Json(new { successMsg, errorMsg });
 }


</br>
Author - priyanka
