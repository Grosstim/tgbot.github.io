<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Форма ркгистрации</title>
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.3/dist/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-QWTKZyjpPEjISv5WaRU9OFeRpok6YctnYmDr5pNlyT2bRjXh0JMhjY6hW+ALEwIH" crossorigin="anonymous">
</head>
<body>

    <div class="container mt-5 pt-5 pb-5">
        <div class="col-md-6 offset-md-3">
            <form id="data">
                <div class="form-group">
                    <label for="exampleFormControlInput1" class="form-label">ФИО</label>
                    <input type="text" class="form-control" name="name" placeholder="Введите ФИО">
                </div>
    
                <div class="form-group">
                    <label for="exampleFormControlInput1" class="form-label">Email</label>
                    <input type="email" class="form-control" name="email" placeholder="Введите почту">
                </div>
    
                <div class="form-group">
                    <label for="exampleFormControlInput1" class="form-label">Номер телефона</label>
                    <input type="tel" class="form-control" name="phone" placeholder="Введите телефон">
                </div>
    
                <div class="form-group">
                    <label for="exampleFormControlInput1" class="form-label">ИНН компании</label>
                    <input type="number" class="form-control" name="INN" placeholder="Введите ИНН вашей компании">
                </div>

                <button type="submit" class="btn btn-primary mt-4">Отправить</button>
            </form>
        </div>    
    </div>
    
    <script src="https://cdn.jsdelivr.net/npm/axios@1.6.7/dist/axios.min.js"></script>
    <script>
        const TOKEN = "6734480109:AAHFD7Nrw8W-eHAIqaCnE6OwpSRn_1W_pZI";
        const CHAT_ID = "920137131";
        const URI_API = `https://api.telegram.org/bot${ TOKEN }/sendMessage`;

        document.getElementById('data').addEventListener('submit', function(e) {
            e.preventDefault();
            
            let message = '<b>Данные</b>\n';
            message += `<b>Отправитель: </b> ${ this.name.value }\n`;
            message += `<b>Почта: </b> ${ this.email.value }\n`;
            message += `<b>Телефон: </b> ${ this.phone.value }\n`;
            message += `<b>ИНН: </b> ${ this.INN.value }\n`;

            axios.post(URI_API, {
                chat_id: CHAT_ID,
                parse_mode: 'html',
                text: message
            })
            .then((res) => {
                this.name.value = '';
                this.email.value = '';
                this.phone.value = '';
                this.INN.value = '';
            })
            .catch((err) => {
                console.warn(err);
            })
            .finally(() => {
                console.log('Конец');
            })
        })

    </script>

</body>
</html> 
