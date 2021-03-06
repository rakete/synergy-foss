# synergy -- mouse and keyboard sharing utility
# Copyright (C) 2012 Bolton Software Ltd.
# Copyright (C) 2009 Nick Bolton
# 
# This package is free software; you can redistribute it and/or
# modify it under the terms of the GNU General Public License
# found in the file COPYING that should have accompanied this file.
# 
# This package is distributed in the hope that it will be useful,
# but WITHOUT ANY WARRANTY; without even the implied warranty of
# MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
# GNU General Public License for more details.
#
# You should have received a copy of the GNU General Public License
# along with this program.  If not, see <http://www.gnu.org/licenses/>.

set(h
	synergy/CKeyStateTests.h
	synergy/CMockEventQueue.h
	synergy/CMockKeyMap.h
	client/CMockClient.h
	io/CMockStream.h
	server/CMockServer.h
	io/CMockCryptoStream.h
	synergy/CMockScreen.h
	server/CMockConfig.h
	server/CMockPrimaryClient.h
	server/CMockInputFilter.h
)

set(src
	${h}
	Main.cpp
	synergy/CClipboardTests.cpp
	synergy/CKeyStateTests.cpp
	client/CServerProxyTests.cpp
	synergy/CCryptoStreamTests.cpp
	server/CClientProxyTests.cpp
)

set(inc
	../../lib/arch
	../../lib/base
	../../lib/client
	../../lib/server
	../../lib/common
	../../lib/io
	../../lib/mt
	../../lib/net
	../../lib/platform
	../../lib/synergy
	../../../tools/gtest-1.6.0/include
	../../../tools/gmock-1.6.0/include
	../../../tools
	io
	synergy
)

if (UNIX)
	list(APPEND inc
		../../..
	)
endif()

if (WIN32)
	if (GAME_DEVICE_SUPPORT)
		link_directories("$ENV{DXSDK_DIR}/Lib/x86")
	endif()
endif()

include_directories(${inc})
add_executable(unittests ${src})
target_link_libraries(unittests
	arch base client server common io net platform server synergy mt gtest gmock cryptopp ${libs})
