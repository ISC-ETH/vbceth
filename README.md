# ETH-Contract

The world's leading technology, today's DAPP trend has arrived

# ABOUT VBC-ETH

Vbc-eth contract is the only DAPP technology application developed by the technology team led by vitalik buterin, the founder of Ethereum in 48 months. It is also the only contract based income DAPP application in the world. The income and output are all built on the trust public chain. It is the only DAPP application based on the ETH public chain. It is also the only one in the world A revenue platform based on the contract system, which solves the trust relationship between investors and the platform, and adopts an electronic contract that cannot be tampered with, which will be a new revolution in the global blockchain financial market.

# Contract Profit Source

The project platform comes from multiple sources of income. Futures leverage contracts participate in the futures trading of ether currency and obtain fixed returns. When we invest in community contracts, we can't use them all as nodes, because the profits of nodes are not enough for us to share. At present, most of the funds will be used for arbitrage trading. For example, when selling 248 usdt, there will be 10000 eth, i.e. 2.48 million usdt; when retrieving 218 usdt, 2.48 million yuan = 11.3 million eth, and the net profit will be 130 eth. As long as the market goes up and down, there must be margin. Once there is profit, there must be profit. Our advantages are: with many chips, you can smash and pull. Between smashing and pulling, you can naturally earn the number of eth. We invest in global nodes in super node award contracts. At the same time, the platform uses global Ethereum entertainment guessing game to make more Ethereum nodes active, so as to improve the actual application of Ethereum. Of course, we can also let Ethereum participate in the game to bring Everyone entertainment, thanks for the participation of global players!

# Contract revenue

The platform adopts the rules of the game of global booking, order grabbing and control mode. The platform adopts the mode of first paying deposit, then order grabbing and balance payment for all players, and then paying deposit 7 days later to reward the last round of principal and interest. 7% per principal plus interest. Register successfully as one star member and enjoy 100% of the direct recommendation revenue of the generation! For example, if you recommend me, I can earn 30 eth per month, and you can earn 30 eth per month. If you recommend 100 people, the first generation will earn 3000 eth per month. Eth multiplied by the real-time price of the exchange is your actual return. Two star members need conditions, direct promotion needs to push the standard of 3 effective members, 10 effective members of team umbrella team, enjoy 40% of the second generation's income. After two stars, it is easy to earn 20-60 eth every month. Samsung members need conditions. Three of the members recommended directly are two-star members, which will reach Samsung members. Samsung members enjoy 20% of the third generation income. Four star standard conditions, directly recommend four two-star members to directly meet the standard of four-star members. Four stars enjoy 2% of the fourth generation's income. 5 2-star members are directly recommended as 5-star members according to the five-star standard conditions. 5-star members can enjoy 2% of the income of the fourth generation as well as unlimited 2% of the income. The final six-star evaluation condition is that I am a five-star member, and two members of my team who are directly promoted to five-star will reach the six-star level. In addition to enjoying 100% of the first generation, 40% of the second generation, 20% of the third generation, 2% of the fourth generation and 2% of the infinite generation. I'll reward you 60 eth again.

# Part of code

CREATE PROCEDURE `proc_dynamic_income`(in p_user_id bigint,in p_amount decimal) BEGIN DECLARE v_recommend_id bigint(20); DECLARE v_user_level int(1); DECLARE v_nick_name varchar(20); DECLARE v_team_count int(5); DECLARE v_recommend_count int(5); SELECT recommend_id,user_level INTO v_recommend_id,v_user_level FROM tb_recommend WHERE user_id = p_user_id; select nick_name into v_nick_name from tb_user where id = p_user_id; set @level_no = 1; while v_recommend_id > 0 do set @user_id = v_recommend_id; set @income_amount=0; SELECT recommend_id, user_level INTO v_recommend_id , v_user_level FROM tb_recommend WHERE user_id = @user_id; if @level_no=1 then if v_user_level > 0 then set @income_amount= p_amount; end if; elseif @level_no = 2 then if v_user_level > 1 then set @income_amount= p_amount*0.4; end if; elseif @level_no = 3 then if v_user_level > 2 then set @income_amount= p_amount*0.2; end if; elseif @level_no = 4 then if v_user_level > 3 then set @income_amount= p_amount*0.02; end if; else if v_user_level > 4 then set @income_amount= p_amount*0.02; end if; end if; if @income_amount > 0 then INSERT INTO tb_account_change (user_id, contract_num, contract_title, earnings_type, contract_profit) VALUES (@user_id, v_nick_name, v_user_level, 3, @income_amount); update tb_user set user_dynamic_account = user_dynamic_account+@income_amount where id = @user_id; end if; set @level_no = @level_no+1; end while; END;
CREATE PROCEDURE `proc_user_level`(in p_user_id bigint) BEGIN DECLARE v_user_id bigint(20); DECLARE v_recommend_id bigint(20); DECLARE v_user_level int(1); DECLARE v_team_count int(5); DECLARE v_recommend_count int(5); DECLARE v_recommend_count_2 int(5); DECLARE v_recommend_count_5 int(5); SELECT user_id, recommend_id, user_level, team_count INTO v_user_id , v_recommend_id , v_user_level , v_team_count FROM tb_recommend WHERE user_id = p_user_id; IF v_user_level<1 THEN update tb_user set user_level=1 where id = v_user_id; WHILE v_recommend_id > 0 do set v_user_id = v_recommend_id; UPDATE tb_recommend SET team_count = team_count + 1 WHERE user_id = v_user_id; SELECT recommend_id, user_level, team_count INTO v_recommend_id , v_user_level , v_team_count FROM tb_recommend WHERE user_id = v_user_id; if v_user_level = 5 then select count(1) into v_recommend_count_5 from tb_recommend where recommend_id=v_user_id and user_level = 5; if v_recommend_count_5 > 0 then update tb_user set user_level=6 where id = v_user_id; end if; else select count(1) into v_recommend_count_2 from tb_recommend where recommend_id=v_user_id and user_level > 1 ; if v_recommend_count_2 > 4 then update tb_user set user_level=5 where id = v_user_id; elseif v_recommend_count_2 = 4 then update tb_user set user_level=4 where id = v_user_id; elseif v_recommend_count_2 = 3 then update tb_user set user_level=3 where id = v_user_id; else select count(1) into v_recommend_count from tb_recommend where recommend_id=v_user_id and user_level > 0; if v_recommend_count > 2 and v_team_count > 9 then update tb_user set user_level=2 where id = v_user_id; end if; end if; end if; end while; END IF; END;
