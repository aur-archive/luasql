# Maintainer: perlawk

pkgname=luasql
pkgver=2.3.0
pkgrel=2
pkgdesc='LuaSQL is a simple interface from Lua to a DBMS. Here sqlite3, mysql, postgres are included for Lua 5.1/5.2.'
arch=('i686' 'x86_64')
url='http://www.keplerproject.org/luasql/'
license=('MIT')
depends=('lua' 'lua51' 'sqlite3' 'mariadb-clients' 'postgresql')
source=("https://codeload.github.com/keplerproject/luasql/tar.gz/v2.3.0")

build() {
	cd $srcdir/luasql-$pkgver/src
	mkdir -p 5.1 5.2
	gcc -fpic -c -I/usr/include/lua5.1 -I/usr/include/mysql luasql.c ls_sqlite3.c ls_mysql.c ls_postgres.c
	gcc -shared -o 5.1/sqlite3.so luasql.o ls_sqlite3.o -lsqlite3 -I/usr/include/lua5.1 -llua5.1
	gcc -shared -o 5.1/mysql.so luasql.o ls_mysql.o -lmysqlclient -I/usr/include/lua5.1 -llua5.1 -lz
	gcc -shared -o 5.1/postgres.so luasql.o ls_postgres.o -lpq -I/usr/include/lua5.1 -llua5.1

	gcc -fpic -c -I/usr/include/lua -I/usr/include/mysql luasql.c ls_sqlite3.c ls_mysql.c ls_postgres.c
	gcc -shared -o 5.2/sqlite3.so luasql.o ls_sqlite3.o -lsqlite3 -llua
	gcc -shared -o 5.2/mysql.so luasql.o ls_mysql.o -lmysqlclient -llua -lz
	gcc -shared -o 5.2/postgres.so luasql.o ls_postgres.o -lpq -llua
}

package() {
	cd $srcdir/luasql-$pkgver/src
	loc="$pkgdir"/usr/lib/lua/5.
	mkdir -p "$loc"1/luasql "$loc"2/luasql

	cd 5.1; cp sqlite3.so mysql.so postgres.so "$loc"1/luasql
	cd ../5.2; cp sqlite3.so mysql.so postgres.so "$loc"2/luasql
}
md5sums=('af9f0f3a2313a1fcf88c40700092048d')
