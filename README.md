
BigDecimalInt BigDecimalInt::operator- (BigDecimalInt anotherDec){
    if(value=="0"){
        if(anotherDec.sign=='-')anotherDec.sign='+';
        else anotherDec.sign='-';
        return anotherDec;
    }
    else if(anotherDec.value=="0"){
        BigDecimalInt temp("");
        temp.sign=sign;
        temp.value=value;
        return temp;
    }
    else if(sign==anotherDec.sign){
        long long com_length=max(value.size(),anotherDec.value.size());
         BigDecimalInt sum2("0");
        string to_10scom;
        if(sign=='-'){
            to_10scom=value;
           sum2.value=anotherDec.value;
           sum2.sign=anotherDec.sign;
            }
        else{
            to_10scom=anotherDec.value;
           sum2.value=value;
           sum2.sign=sign;
            }
        long long to_10scom_length=to_10scom.length();
        string _10scom="";
        for(long long i=to_10scom_length-1;i>=0;i--){
            _10scom=char('9'-to_10scom[i]+'0')+_10scom;
        }
        for(long long i=0;i<(com_length-to_10scom_length);i++){
            _10scom='9'+_10scom;
        }
        int carry=0;
        bool first=true;
        for(long long i=_10scom.length()-1;i>=0;i--){
            if(_10scom[i]+carry>='9'){
                   
                    _10scom[i]='0';
                     carry=1;
                     first=false;
            }
            else {
                _10scom[i]=_10scom[i]+carry;
                if(first)_10scom[i]+=1;
                break ;
            }
        }
        BigDecimalInt bid_10scom(_10scom);
        BigDecimalInt sub=bid_10scom+sum2;
        if(sub.value.length()>_10scom.length()){
            sub.value.erase(0,1);
            return sub;
        }
        else {
            sub.sign='-';
            string temp_value="";
            for(long long i=sub.value.length()-1;i>=0;i--){
                temp_value=char('9'-sub.value[i]+'0')+temp_value;
            }
            cout<<endl<<temp_value;
            int carry =0;
            bool first=true;
            for(long long i=temp_value.length()-1;i>=0;i--){
            if(temp_value[i]+carry>='9'){
                 temp_value[i]='0';
                    carry=1;
                    first=false;
                   
            }
            else {
                temp_value[i]=temp_value[i]+carry;
                if(first)temp_value[i]+=1;
                break ;
                 }
            }
            sub.value=temp_value;
            return sub;
        }


    }
    else {
        BigDecimalInt _temp(value);
        BigDecimalInt sub=_temp+anotherDec;
        return sub;
    }
    
}
bool BigDecimalInt :: operator< (BigDecimalInt anotherDec){
    if(anotherDec.sign==sign){
        long long anotherDec_lenght=anotherDec.value.length();
        long long this_length=value.length();

        if(this_length==anotherDec_lenght){
            for(long long i=0;i<this_length;i++){
                if(value[i]!=anotherDec.value[i]){
                    if(value[i]<anotherDec.value[i]){
                        if(sign=='+')return true;
                        else return false;
                    }
                    else {
                        if(sign=='-')return true;
                        else return false;
                    }
                }
            }
            return false;
        }
        else if(sign=='+'){
            if(this_length<anotherDec_lenght)return true;
            else return false;
        }
        else {
             if(this_length>anotherDec_lenght)return true;
            else return false;
        }
    }
    else{
        if(anotherDec.sign=='+')return true;
        else return false;
    }
}

