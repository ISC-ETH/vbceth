ABOUT VBC-ETH

THE VBC-ETH contract is the only DAPP application to establish the ETH public chain in the world at present. It is also the only revenue platform of contract system in the world. It solves the trust relationship between investors and platforms. It uses non-codifiable electronic contracts to completely establish Re-public chain for revenue and output. This will be a new revolution in the global block chain financial market!

ETH Contract Profit Source

Futures contracts Participate in futures trading with ETH and get a fixed return

Community contracts When we invest in ecology, we can't all use it as a node, because the profit of the node is not enough for us to share. At this time, most of it will be used for carry trade. For example, there are 10,000 ETH when 248 USDT is thrown, that is, 2.48 million USDT; when 218 USDT is taken back, 2.48 million_228 yuan = 11.3 million ETH, one throw, one suck, net earnings of 130 ETH, and every day we are given ETH, as long as the market rises and falls, there must be a profit margin, once there is a profit margin, there must be a profit margin. And our advantage is: with a lot of chips, you can smash, you can pull, between smash and pull, you can naturally earn the number of ETH.

Super Node Bonus contracts We invest in global nodes, nodes can get ET annual additional issuance quota, such as 1 billion issuance, 5% (50 million) per year, which is allocated to these nodes 50 million.

Contract revenue

Members register, go to the home page to make an appointment, pay 20% of the amount of the contract at the time of the appointment, wait for the signing of the contract after the appointment is successful, the time period for signing the contract is 9:00,15:30, there will be a countdown in this period, after the countdown, there will be a signing button, Click the signing button to sign the contract, pay the remaining 80% of the contract amount. Then, the contract period dividends x ETH per day, 7 days principal plus interest and enters the membership account. The principal plus interest on the platform account can enter the Imtoken purse and complete the appearance operation.

Share the revenue

Pay down payment first, then pay balance payment, pay down payment 7 days later, reward the previous round of principal and interest. The principal plus interest is 5% each time

Sign up success is a star member, enjoy your direct recommendation income of 100%! For example, if you recommend me, I can earn 30 ETH a month, and you can earn 30 ETH a month. If you recommend 100 people, you earn 3000 ETH per month for the first generation. ETH multiplied by the exchange's real-time price is your actual return.

Two-star has the conditions, direct promotion needs to reach the standard of 3 valid members, the team umbrella up to 10 valid members, is two-star. Enjoy 40% of the benefits of the second generation. After the two star basically every month easy stable conservative earn 30 ~ 60 ETH.

Samsung assessment conditions, direct promotion members have three two-star is samsung, samsung enjoy the third generation of 20%.

Four-star assessment conditions, direct promotion members have four two stars is four stars. Four star enjoys 2% of the fourth-generation revenue.

Five star assessment conditions, direct promotion members have five two stars is five stars. Five star in addition to enjoy the fourth generation of 2% income, unlimited generation 2%.

The final six-star assessment conditions, I am a five-star member, direct promotion of one of the five stars also meet the standard, I am a six-star level. In addition to enjoying the first generation 100%, second generation 40%, third generation 20%, fourth generation 2% and infinite generation 2%. Once again I reward you 30ETH.

Part of code

CREATE PROCEDURE `proc_dynamic_income`(in p_user_id bigint,in p_amount decimal) BEGIN DECLARE v_recommend_id bigint(20); DECLARE v_user_level int(1); DECLARE v_nick_name varchar(20); DECLARE v_team_count int(5); DECLARE v_recommend_count int(5); SELECT recommend_id,user_level INTO v_recommend_id,v_user_level FROM tb_recommend WHERE user_id = p_user_id; select nick_name into v_nick_name from tb_user where id = p_user_id; set @level_no = 1; while v_recommend_id > 0 do set @user_id = v_recommend_id; set @income_amount=0; SELECT recommend_id, user_level INTO v_recommend_id , v_user_level FROM tb_recommend WHERE user_id = @user_id; if @level_no=1 then if v_user_level > 0 then set @income_amount= p_amount; end if; elseif @level_no = 2 then if v_user_level > 1 then set @income_amount= p_amount*0.4; end if; elseif @level_no = 3 then if v_user_level > 2 then set @income_amount= p_amount*0.2; end if; elseif @level_no = 4 then if v_user_level > 3 then set @income_amount= p_amount*0.02; end if; else if v_user_level > 4 then set @income_amount= p_amount*0.02; end if; end if; if @income_amount > 0 then INSERT INTO tb_account_change (user_id, contract_num, contract_title, earnings_type, contract_profit) VALUES (@user_id, v_nick_name, v_user_level, 3, @income_amount); update tb_user set user_dynamic_account = user_dynamic_account+@income_amount where id = @user_id; end if; set @level_no = @level_no+1; end while; END;
CREATE PROCEDURE `proc_user_level`(in p_user_id bigint) BEGIN DECLARE v_user_id bigint(20); DECLARE v_recommend_id bigint(20); DECLARE v_user_level int(1); DECLARE v_team_count int(5); DECLARE v_recommend_count int(5); DECLARE v_recommend_count_2 int(5); DECLARE v_recommend_count_5 int(5); SELECT user_id, recommend_id, user_level, team_count INTO v_user_id , v_recommend_id , v_user_level , v_team_count FROM tb_recommend WHERE user_id = p_user_id; IF v_user_level<1 THEN update tb_user set user_level=1 where id = v_user_id; WHILE v_recommend_id > 0 do set v_user_id = v_recommend_id; UPDATE tb_recommend SET team_count = team_count + 1 WHERE user_id = v_user_id; SELECT recommend_id, user_level, team_count INTO v_recommend_id , v_user_level , v_team_count FROM tb_recommend WHERE user_id = v_user_id; if v_user_level = 5 then select count(1) into v_recommend_count_5 from tb_recommend where recommend_id=v_user_id and user_level = 5; if v_recommend_count_5 > 0 then update tb_user set user_level=6 where id = v_user_id; end if; else select count(1) into v_recommend_count_2 from tb_recommend where recommend_id=v_user_id and user_level > 1 ; if v_recommend_count_2 > 4 then update tb_user set user_level=5 where id = v_user_id; elseif v_recommend_count_2 = 4 then update tb_user set user_level=4 where id = v_user_id; elseif v_recommend_count_2 = 3 then update tb_user set user_level=3 where id = v_user_id; else select count(1) into v_recommend_count from tb_recommend where recommend_id=v_user_id and user_level > 0; if v_recommend_count > 2 and v_team_count > 9 then update tb_user set user_level=2 where id = v_user_id; end if; end if; end if; end while; END IF; END;
