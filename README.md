# Openwrt_compat

이 프로젝트는 compat-wireless-2014-05-22 안에 있는 자료들이다.
수정한 코드는 driver/net/wireless/ath/ath9k 에 있는 xmit.c이다.
git clone으로 이 프로젝트를 받은 뒤, 원래 있는 openwrt의 xmit.c와 바꾼 후, make를 하면 된다.
module은 scp로 compat, cfg80211, mac80211, ath, ath9k_hw, ath9k_common, ath9k를 ap에 전송한다.
root@OpenWrt # rmmod ath9k
root@OpenWrt # rmmod ath9k_common
root@OpenWrt # rmmod ath9k_hw
root@OpenWrt # rmmod ath ok
root@OpenWrt # rmmod mac80211
root@OpenWrt # rmmod cfg80211
root@OpenWrt # rmmod compat

rmmod를 한 후, 위의 모듈을 순서를 반대로 insmod한다.

테스트 방법:
ethernet으로 연결한 노트북에서 위의 방법대로 모듈을 올린 뒤, /etc/init.d/network restart.
wireless lan으로 연결된 노트북에서 client 실행.
그 노트북에서 터미널을 하나 더 띄운 후, ssh로 ap에 접속하여 tcpdump -i wlan# -xnS > a.out 실행.
a.out 파일안에 tcp packet 전송 정보를 보면 된다.
