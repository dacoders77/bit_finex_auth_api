# bit_finex_auth_api
Access www.bitfinex.com auth api endpoints via Laravel 5.5 and Guzzle

Example of how to place a new order on www.bitfinex.com 
Order parameters are described here: https://bitfinex.readme.io/v1/reference#rest-auth-new-order

Request is made this simple way: 

    public function requestPrepare($summary, $volume, $direction) {

        // Assign key values
        $this->api_key = $_ENV['BIT_FINEX_PUBLIC_API_KEY']; // Api keys go here
        $this->api_secret = $_ENV['BIT_FINEX_PRIVATE_API_KEY']; // Add them to .env file or in "***"

        // This method call can take two parameters
        // No params taken. Only first value is sent
        $request = $this->endpoint($summary);

        $data = array(
            'request' => $request, 
            'symbol'=> 'ETHUSD', // ETHUSD ETCUSD
            'amount' => $volume, // 0.02
            'price' => '1000',
            'exchange' => 'bitfinex',
            'side' => $direction,
            // exchange market - exchanger order. market - margin order. If you need to open a short position - use 'market'. It is                   impossible to go short with 'exchange order'
            // Funds must be located at Margin wallet if you go short and long.
            'type' => 'market'
        );

        return $this->send_auth_request($data);
    }
    
    The logic was taken form here: https://github.com/mariodian/bitfinex-auto-lend/blob/master/bitfinex.php 
    The CURL was replaced with Guzzle which made the solution light and easy. 
    
    

