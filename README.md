# Asp.net-.aspx-webrequest-Hit-

# Asp.net .aspx webrequest Hit 


```
 private bool? CheckValidEmail(string emailID, string productID)
        {
            productregisterdtbl productregisterdtbl = this._db.productregisterdtbls.Where<productregisterdtbl>((Expression<Func<productregisterdtbl, bool>>)(m => m.ProductName == emailID && m.Status == 1 && m.ProductID == new Guid(productID))).SingleOrDefault<productregisterdtbl>();
            if (productregisterdtbl != null && (productregisterdtbl.LiecenceLimit>0 && productregisterdtbl.LiecenceLimit.Value>0))
            {
                short? nullable1 = productregisterdtbl.Used;
                short? nullable2 = nullable1;
                if (!(nullable2.HasValue ? new int?((int)nullable2.GetValueOrDefault()) : new int?()).HasValue)
                    nullable1 = new short?((short)0);
                short? nullable3 = nullable1;
                short? limit = productregisterdtbl.Limit;
                if (((int)nullable3.GetValueOrDefault() > (int)limit.GetValueOrDefault() ? 0 : (nullable3.HasValue & limit.HasValue ? 1 : 0)) == 0)
                    return new bool?(false);
                this.lLimit = true;
                return Convert.ToBoolean(productregisterdtbl.Status);
            }
            return new bool?(this._db.productregisterdtbls.Any<productregisterdtbl>((Expression<Func<productregisterdtbl, bool>>)(m => m.ProductName == emailID && m.Status == 1 && m.ProductID == new Guid(productID))));
        }
        ```
            public static bool CheckProduct(string emailId, string productID)
        {
            bool status = false;
            string serialNo = Licence.GetSerialNo();
            var data = Licence.Gethtml(Licence._register + serialNo.Trim() + "&EmailID=" + emailId + "&PID=" + productID);
            if (data.Contains("Query Success"))
            {
                status = true;
            }
            return status;
        }

        private static string Gethtml(string a)
        {
            string str;
            try
            {
                //ServicePointManager.Expect100Continue = true;
                //ServicePointManager.SecurityProtocol = SecurityProtocolType.Tls11 | SecurityProtocolType.Tls12;

                HttpWebRequest httpWebRequest = (HttpWebRequest)WebRequest.Create(a);
                httpWebRequest.Method = "GET";
                httpWebRequest.AllowAutoRedirect = true;
                HttpWebResponse response = (HttpWebResponse)httpWebRequest.GetResponse();
                Stream responseStream = response.GetResponseStream();
                Encoding utF8 = Encoding.UTF8;
                StreamReader streamReader = new StreamReader(responseStream, utF8);
                string end = streamReader.ReadToEnd();
                responseStream.Close();
                streamReader.Close();
                response.Close();
                str = end;
            }
            catch (Exception ex)
            {
                //if (Licence.counter < 3)
                //{
                //    ++Licence.counter;
                //    str = Licence.Gethtml(a);
                //}
                //else
                   str = "Error Occured";
            }
            return str;
        }
        ```
